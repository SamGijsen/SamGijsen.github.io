---
title: Can diffusion transformers do in-silico neuroscience?
categories:
- General
sharing: false
excerpt: |
    Generating neural FMRI time series for unseen task conditions with diffusion transformers.
---

In a new preprint, we train models to generate neural (FMRI) time series. We evaluate on hundreds of **unseen** task conditions and check if predicted experimental manipulations match reality.

We use a transformer setup which allows for conditioning per time step by injecting conditioning tokens directly in context. For each time step, we include compositional language tokens of task descriptions as well as optional spatial priors to aid out-of-distribution generation. This allows us to specify task structure flexibly.

<img src="/assets/blog_pinc-flows/methods_overview.png" alt="Methods overview" style="display: block; width: 65%; max-width: 768px; height: auto; margin: 0 auto 2rem;">

Some results:

We find that the model enables counterfactual generation (B,C,D), learns the brain's hemodynamic response function (C), and captures repetition inhibition (D) - a well established finding in neuroscience.

<img src="/assets/blog_pinc-flows/counterfactuals.png" width="768" alt="Counterfactual FMRI generation results" style="display: block; margin-bottom: 2rem;">

Next, we generate time series for unseen tasks and recover activation maps. We find that using compositional language conditioning alone can perform surprisingly well (correlations with real of 0.35-0.60 depending on setup).

<video src="/assets/blog_pinc-flows/denoise_txt.mp4" width="768" controls autoplay muted loop playsinline style="display: block; margin-bottom: 2rem;"></video>

However, OOD performance expectedly degrades with distance to the training support. We therefore train the model to use optional spatial priors in a self-supervised manner. These priors are defined per event or response, can be obtained from existing datasets, and then re-composed for counterfactual experiments.

<video src="/assets/blog_pinc-flows/event_mixing.mp4" controls autoplay muted loop playsinline style="display: block; width: 85%; max-width: 768px; height: auto; margin: 0 auto 2rem;"></video>

We confirm that using spatial priors yield better OOD performance further from the training support where language-only conditioning struggles (increasing correlations with real up to 0.88).

<video src="/assets/blog_pinc-flows/spat_vs_txt.mp4" width="768" controls autoplay muted loop playsinline style="display: block; margin-bottom: 2rem;"></video>

We quantify training support distance in terms of both spatial activation maps and language embeddings of task descriptions, both showing distinct degradation profiles.

<img src="/assets/blog_pinc-flows/train_support_distance.png" width="768" alt="Training support distance analyses" style="display: block; margin-bottom: 2rem;">

This constitutes just a first step towards in silico experimental design but already works surprisingly well, with tons of open paths for improvements!

Paper [https://arxiv.org/abs/2606.11833](https://arxiv.org/abs/2606.11833)
