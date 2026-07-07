---
title: Label-efficient glucose estimation from semi-synthetic Raman-like measurements
layout: post
permalink: /general/2026/07/07/cgm/
date: 2026-07-07
categories:
- General
sharing: false
hidden: true
sitemap: false
excerpt: |
    A toy study on whether self-supervised learning can improve glucose prediction from Raman spectra and wearable context in unseen subjects.
---

The goal is to predict glucose in unseen subjects from Raman spectra, using additional context variables from wearables. Importantly, this is a calibration-free setting, not using any glucose labels from the test subjects.

Let's look at two potential challenges:

1. Label scarcity: in a supervised setting, learning to predict glucose requires many paired Raman and glucose measurements, which are expensive to obtain.
2. Temporal plausibility: for the predicted trajectories in the [Liom paper](https://journals.sagepub.com/doi/10.1177/19322968251313811), much of the error does not look physiologically impossible. Instead, the predicted trajectories appear insufficiently smooth. Context can help here: for example, intense physical activity can induce rapid glucose changes, so conditioning on context variables may improve calibration.

Self-supervised learning (SSL) can help for both of these challenges.

1. Learning useful representations from unlabeled Raman spectra can improve transfer, requiring fewer supervised pairs for finetuning than a model trained from scratch.
2. Integrating context variables during pretraining lets the model learn how context affects spectra in a self-supervised manner.


### Setup

Broadly, I test this in a toy example as follows:

I use the open BrisT1D dataset to get time series of real longitudinal CGM-derived glucose trajectories paired with context variables (heart rate, steps, distance, calories, discrete activities/sports). We'll treat these CGM values as our expensive labels. 

Then, with the help of 5.5-pro I did a literature search to define a sensible, semi-synthetic data generation process of Raman spectra based on the CGM measurements. We define the relationship between glucose and Raman spectra as lossy, making reverse inference non-trivial. 

Briefly, effectively a legend for the figure below: let $s$ index a subject/group, $t$ a time point, and $\nu$ the Raman-shift or spectral coordinate. $y_{s,t}$ is the real scalar trajectory; $c_{s,t}$ is auxiliary context; and $m_{s,t}$ is the corresponding missingness mask. $x_{s,t}(\nu)$ is the generated Raman-like measurement, built from a target template $T_y$, group background $U_s$, smooth baseline $B_{s,t}$, nuisance templates $T_j$, gain $G_{s,t}$, noise $\varepsilon_{s,t}$, and artifacts $A_{s,t}$. The coefficient $\alpha$ controls target-signal strength, $\delta_{s,t}$ is a small spectral shift, and $a_{j,s,t}$ are nuisance amplitudes. Finally, $r_{s,t}=\sigma(w^\top \mathrm{normalize}(c_{s,t}))$ is a context-derived corruption score that modulates gain, noise, shift, and artifact probability.

<img src="/assets/blog_cgm/data_gen.png" alt="Semi-synthetic Raman data generation process" style="display: block; width: 100%; max-width: 900px; height: auto; margin: 0 auto 2rem;">

This yields (Raman, context, glucose) triples for supervised learning (i.e. (Raman, context) $\rightarrow$ glucose) and (Raman, context, null) triplets for self-supervised learning. Note that glucose is never exposed to the model during SSL. To keep the problem low-dimensional, we use a template bank to extract features from the spectra (glucose, d1, d2, tissue, lactate, urea, power). 

(An initial check showed that a more generic SNV into PCA representation still recovers the signal cross-subject at 26% MADRS, r=0.67, compared to 17% MADRS, r=0.87 using the template bank. The latter makes for a cleaner toy example, as I should note that due to the synthetic glucose relationship, absolute accuracy is not meaningful here; only relative differences between models as a function of labels is.)

<img src="/assets/blog_cgm/group_heldout_estimation_pipeline.png" alt="Group-heldout glucose estimation pipeline" style="display: block; width: 80%; max-width: 760px; height: auto; margin: 0 auto 2rem;">

For SSL, we use a simple MAE setup to train a small causal transformer model. Specifically, given a two hour window with a Raman spectrum every 5 minutes, we mask spans of 3 measurements and we predict the masked values. We mask 6 non-overlapping spans, which masks 72% of all measurements.

<img src="/assets/blog_cgm/ssl_aligned_span_masking.png" alt="Aligned span masking setup for self-supervised learning" style="display: block; width: 100%; max-width: 900px; height: auto; margin: 0 auto 2rem;">

We define a "label scarce" setting by using two subjects and sampling 2000 triplets per subject (i.e. for a total of 4000 triplets) which are available for supervised learning and finetuning, while 12 subjects (24000 samples) are available for SSL.

I find that SSL pretraining following by finetuning yields better cross-subject predictions:

<div class="math-display">
\[
\begin{array}{lccc}
\hline
\textbf{Model} & \textbf{Mean dense MARD} & \textbf{Std across draws} & \textbf{5th-95th percentile} \\
\hline
\text{Supervised} & 22.81\% & 8.25 & 17.75\text{--}32.69 \\
\text{SSL} & 20.10\% & 4.60 & 17.41\text{--}27.60 \\
\hline
\end{array}
\]
</div>

In addition, the model is less sensitive to the randomly drawn labeled subjects (std down to 4.60 from 8.25) with the 95th percentile down from 32.69 to 27.60, which can be a useful calibration-free property.

<!-- <img src="/assets/blog_cgm/SSL_2_vs_all.png" alt="Self-supervised pretraining improves estimation with few labeled subjects" style="display: block; width: 100%; max-width: 900px; height: auto; margin: 0 auto 2rem;">

When looking at the smoothness of predictions, we see my initial hypothesis doesn't hold. True rate of change (RoC) is flat across motion quartiles (left plot; not my personal experience!). The supervised model especially however, predicts trajectories with higher RoC for higher motion - which may be related to motion changing othe optical reliability structure in the simulator. While SSL models are more robust to this efefct, they do tend to overestimate overall RoC still. 

<img src="/assets/blog_cgm/ROC.png" alt="Prediction smoothness" style="display: block; width: 90%; max-width: 900px; height: auto; margin: 0 auto 2rem;"> -->




Error stratification shows us where the improvements lie. The SSL gain seems concentrated in euglycemia (-3.7), while it mostly vanishes in hyperglycemia (-0.1). When glucose is high, the target signal is larger relative to the nuisance in the simulator. As such, it appears the supervised model can already appropriately learn the signal in this regime. Meanwhile, in euglycemia the signal is smaller and "buried", which is where one may expect learning the noise structure from unlabeled spectra is beneficial. The SSL model is also better for hypoglycemia, but data is sparse and neither model does well.

<img src="/assets/blog_cgm/error_stratification.png" alt="Error stratification" style="display: block; width: 90%; max-width: 900px; height: auto; margin: 0 auto 2rem;"> 

How about my hypothesis that context could improve calibration? That doesn't seem to hold for this dataset. Shuffling context values raises MARD by only ~0.3 points for either model, so the spectroscopy features are the main signal and neither model relies on context as a shortcut. I still believe this very much is left open for real data, where context seems genuinely reliability coupled (in ways that the toy simulator here might simply under-express).

Plotting a couple model predictions for two random windows:

<img src="/assets/blog_cgm/model_predictions.png" alt="Model predictions for two randomly selected windows" style="display: block; width: 100%; max-width: 900px; height: auto; margin: 0 auto 2rem;">

As for the synthetic DTS-style error grid, SSL improves both zones (A 50.0% -> 53.6%, A+B 62.0%->66.0%). While the absolute levels are well below clinical CGM performance, the relative differences between supervised and SSL are informative.

<img src="/assets/blog_cgm/DTS.png" alt="DTS" style="display: block; width: 75%; max-width: 900px; height: auto; margin: 0 auto 2rem;">

Finally, let's consider a slightly different setup: rather than having a decent chunk of labels for a couple subjects, what if we have fewer labels for all 12 training subjects? We find a directionally similar result here, and find the performance gap shrinks as sufficient labeled data becomes available.

<img src="/assets/blog_cgm/label_scaling.png" alt="Glucose prediction performance across label-scarce settings" style="display: block; width: 60%; max-width: 540px; height: auto; margin: 0 auto 2rem;">




### Conclusion

I created a toy setup using real (blood glucose, context variables) data for synthetic, Raman-like spectrum generation. Subsequently, I find that unlabeled SSL on (Raman, context variables) data improves cross-subject (i.e. calibration-free) prediction for label scarce regimes.
