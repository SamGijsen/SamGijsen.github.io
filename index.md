---
# title: Dr. Sam Gijsen
# feature_text: |
#   Machine Learning for Clinical Neuroimaging
#   Postdoctoral Researcher
# feature_image: "https://picsum.photos/1300/400?image=989"
---


<section class="profile-intro">
  <div class="profile-intro__copy">
    <h1>Dr. Sam Gijsen</h1>

    <p><strong>Machine Learning Researcher</strong><br>
    Foundation &amp; Generative Models for Physiological Time Series</p>

    Currently a Postdoctoral Researcher at:
    <ul style="margin-top: 0.3em;">
      <li><a>Tübingen AI Center</a></li>
      <li><a href="https://hertie.ai/machine-learning">Hertie Institute for AI in Brain Health</a></li>
    </ul>

    <p>I research multimodal representation learning and build both foundation models as well as generative models for neural and physiological time series. Previously, I completed a PhD in Computational Cognitive Neuroscience (Freie Universität Berlin) on probabilistic inference and worked on pharmaco-imaging at King's College London and Maastricht University.</p>
  </div>

  <img class="profile-intro__photo" src="/assets/profile_pic.jpg" alt="Dr. Sam Gijsen">
</section>

<div class="profile-links">
  {% include button.html text="GitHub" icon="github" link="https://github.com/samgijsen" color="#0366d6" %}
  {% include button.html icon="linkedin" text="LinkedIn" link="https://linkedin.com/in/samgijsen" %}
  {% include button.html icon="scholar" text="Google Scholar" link="https://scholar.google.com/citations?hl=en&user=bSYq9qoAAAAJ" color="#4285F3" %}
</div>

## Recent Work
<hr style="margin: 0.5em 0;">

<div class="title-compact">
  [NeurIPS26] Flow Matching with In-Context Priors for Out-of-Distribution Brain Dynamics
</div>
<section class="featured-work">
  <video class="featured-work__video" autoplay loop muted playsinline>
    <source src="/assets/papers/flow_matching_brain.mp4" type="video/mp4">
  </video>
  <p>We propose a per-timestep conditioned diffusion transformer for generating realistic neural time series during unseen experimental tasks by injecting both compositional language and optional spatial priors in-context. Its zero-shot generation can facilitate counterfactual neuroscience by supporting in-silico design and evaluation of novel cognitive experiments before empirical validation. <a href="/general/2026/06/15/pinc-flows/">A summary with GIFs can be found here.</a></p>
    <p>
      <a href="https://arxiv.org/abs/2606.11833">Paper</a> •
      <a href="https://github.com/SamGijsen/pinc-flows">Code</a> •
      <a href="https://huggingface.co/SamGijsen/pinc-flows">Pretrained Models</a>
    </p>
</section>



<hr style="margin: 2.5em 0;">

<div class="title-compact">
  [ICLR26] Brain-Semantoks: Learning Semantic Tokens of Brain Dynamics with a Self-Distilled Foundation Model
  <span>Sam Gijsen, Marc-André Schulz, Kerstin Ritter</span>
</div>
<section class="work-entry">
  <img class="work-entry__media work-entry__media--small" src="/assets/papers/semantoks_tokenizer.png" alt="Brain-Semantoks tokenizer overview">
  <div class="work-entry__body">
    <p> We develop a self-distilled foundation model for brain dynamics that pretrains in 2 hours and eliminates the need for finetuning. We stabilize self-distillation for noisy time series through learned tokenization, and find log-linear scaling laws for pretraining data on cross-dataset downstream tasks.</p>
    <p>
      <a href="https://arxiv.org/abs/2512.11582">ICLR Paper</a> •
      <a href="https://github.com/SamGijsen/Brain-Semantoks">Code</a> •
      <a href="https://huggingface.co/SamGijsen/Brain-Semantoks">Pretrained Models</a>
    </p>
  </div>
</section>

<hr style="margin: 2.5em 0;">

<div class="title-compact">
  [ICML25] EEG-Language Pretraining for Highly Label-Efficient Clinical Phenotyping
  <span>Sam Gijsen, Kerstin Ritter</span>
</div>
<section class="work-entry">
  <img class="work-entry__media work-entry__media--xlarge" src="/assets/papers/ELM.png" alt="EEG-Language model overview">
  <div class="work-entry__body">
    <p> First-of-its-kind EEG-language model for downstream clinical tasks. We show a multiple-instance learning extension of the infoNCE loss enables multimodal models which align physiological time series with natural language, yielding more useful representations.</p>
    <p>
      <a href="https://arxiv.org/abs/2409.07480">ICML Paper</a> •
      <a href="https://github.com/SamGijsen/ELM">Code</a> •
      <a href="https://github.com/SamGijsen/ELM/tree/main/pretrained">Pretrained Models</a>
    </p>
  </div>
</section>

<hr style="margin: 2.5em 0;">

<div class="title-compact">
  2025 NeurIPS EEG Competition: 7th / 1,183 teams
</div>
<section class="work-entry">
  <img class="work-entry__media work-entry__media--small" src="/assets/papers/eeg_challenge.png" alt="EEG competition visual summary">
  <div class="work-entry__body">
    <p> Led a small team that placed highly using a multi-modal fusion architecture designed from scratch, without any pretraining. Code and report to come!</p>
    <p>
      <a href="https://eeg2025.github.io/leaderboard/">Challenge Link</a> 
    </p>
  </div>
</section>

<hr style="margin: 2.5em 0;">

## Some Previous Work
<hr style="margin: 0.5em 0;">

<div class="title-compact">
  Neural surprise in somatosensory Bayesian learning
  <span>Sam Gijsen, Miro Grundei, Robert T. Lange, Dirk Ostwald, Felix Blankenburg</span>
</div>
<section class="work-entry">
  <img class="work-entry__media work-entry__media--wide" src="/assets/papers/neural_surprise.png" alt="Neural surprise analyses">
  <div class="work-entry__body">
    <p>Computational modeling of neural signals using information-theoretic measures shows perceptual learning can be described as a process of probabilistic inference.</p>
    <p>
      <a href="https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1008068">PLOS Computational Biology</a> • 
      <a href="https://github.com/SamGijsen/SurpriseInSomesthesis">Code</a> 
    </p>
  </div>
</section>

<hr style="margin: 0.5em 0;">

<div class="title-compact">
  Active inference and the two-step task
  <span>Sam Gijsen, Miro Grundei, Felix Blankenburg</span>
</div>
<section class="work-entry">
  <img class="work-entry__media work-entry__media--large" src="/assets/papers/twostep.png" alt="Active inference two-step task figure">
  <div class="work-entry__body">
    <p>We develop active inference models using probabilistic surprise minimization and show these to describe human sequential decision-making better compared to reinforcement learning.</p>
    <p>
      <a href="https://www.nature.com/articles/s41598-022-21766-4">Scientific Reports</a> • 
      <a href="https://github.com/SamGijsen/AI2step">Code</a> 
    </p>
  </div>
</section>

<hr style="margin: 2.5em 0;">

## Latest Blog post

<section class="work-entry">
  <img class="work-entry__media work-entry__media--medium" src="/assets/HillsbradDiffusion/morph_15fps.gif" alt="Hillsbrad diffusion animation">
  <div class="work-entry__body">
    <p><strong>Hillsbrad Diffusion: A World Diffusion Model Criminally Undertrained</strong><br> A qualitative look at a world diffusion model undertrained on two hours of sparse exploration of a large map.</p>
    <p>
      <a href="https://samgijsen.github.io/general/2025/01/27/HillsbradDiffusion">Blog post</a> 
    </p>
  </div>
</section>

<hr style="margin: 0.5em 0;">
