---
# title: Dr. Sam Gijsen
# feature_text: |
#   Machine Learning for Clinical Neuroimaging
#   Postdoctoral Researcher
# feature_image: "https://picsum.photos/1300/400?image=989"
---


<div style="display: flex; align-items: center; gap: 20px; margin-bottom: 1em;">
  <div>
    <h1 style="margin-bottom: 0.2em;">Dr. Sam Gijsen</h1>

    <p><strong>Machine Learning Researcher</strong><br>
    Representation Learning &amp; Multimodal Modeling<br>for Biological Time Series</p>

    Currently a Postdoctoral Researcher at:
    <ul style="margin-top: 0.3em;">
      <li><a>Tübingen AI Center</a></li>
      <li><a href="https://hertie.ai/machine-learning">Hertie Institute for AI in Brain Health</a></li>
    </ul>

    <p>I research multimodal representation learning and build foundation models for neural and physiological time series. Previously, I completed a PhD in Computational Cognitive Neuroscience (Freie Universität Berlin) and worked on pharmaco-imaging at King's College London and Maastricht University.</p>
  </div>

  <img src="/assets/profile_pic.jpg" alt="Dr. Sam Gijsen" style="width: 200px; height: 200px; border-radius: 50%; object-fit: cover; margin-left: 2em;">
</div>

{% include button.html text="GitHub" icon="github" link="https://github.com/samgijsen" color="#0366d6" %} {% include button.html icon="linkedin" text="LinkedIn" link="https://linkedin.com/in/samgijsen" %} {% include button.html icon="scholar" text="Google Scholar" link="https://scholar.google.com/citations?hl=en&user=bSYq9qoAAAAJ" color="#4285F3" %}

## Recent Work
<hr style="margin: 0.5em 0;">

<div class="title-compact">
  [ICLR26] Brain-Semantoks: Learning Semantic Tokens of Brain Dynamics with a Self-Distilled Foundation Model
  <span>Sam Gijsen, Marc-André Schulz, Kerstin Ritter</span>
</div>
<div style="display: flex; gap: 20px; margin-bottom: 2em;">
  <img src="/assets/papers/semantoks_tokenizer.png" alt="Project 2" style="width: 150px; object-fit: cover;">
  <div>
    <p> We develop a self-distilled foundation model for brain dynamics that pretrains in 2 hours and eliminates the need for finetuning. We stabilize self-distillation for noisy neural time series through learned tokenization, and find log-linear scaling laws for pretraining data on cross-dataset downstream tasks.</p>
    <p>
      <a href="https://arxiv.org/abs/2512.11582">ICLR Paper</a> •
      <a href="https://github.com/SamGijsen/Brain-Semantoks">Code</a> •
      <a href="https://huggingface.co/SamGijsen/Brain-Semantoks">Pretrained Models</a>
    </p>
  </div>
</div>

<hr style="margin: 2.5em 0;">

<div class="title-compact">
  [ICML25] EEG-Language Pretraining for Highly Label-Efficient Clinical Phenotyping
  <span>Sam Gijsen, Kerstin Ritter</span>
</div>
<div style="display: flex; gap: 20px; margin-bottom: 2em;">
  <img src="/assets/papers/ELM.png" alt="Project 2" style="width: 350px; object-fit: cover;">
  <div>
    <p> First-of-its-kind EEG-language model for downstream clinical tasks. We show that multimodal models integrating natural language learn more useful representations of neural data.</p>
    <p>
      <a href="https://arxiv.org/abs/2409.07480">ICML Paper</a> •
      <a href="https://github.com/SamGijsen/ELM">Code</a> •
      <a href="https://github.com/SamGijsen/ELM/tree/main/pretrained">Pretrained Models</a>
    </p>
  </div>
</div>

<hr style="margin: 2.5em 0;">

<div class="title-compact">
  2025 NeurIPS EEG Competition: 7th / 1,183 teams
</div>
<div style="display: flex; gap: 20px; margin-bottom: 2em;">
  <img src="/assets/papers/eeg_challenge.png" alt="Project 2" style="width: 150px; object-fit: cover;">
  <div>
    <p> Led a small team that placed highly using a multi-modal fusion architecture designed from scratch, without any pretraining. Code and report to come!</p>
    <p>
      <a href="https://eeg2025.github.io/leaderboard/">Challenge Link</a> 
    </p>
  </div>
</div>

<hr style="margin: 2.5em 0;">

## Latest Blog post

<!-- <div class="title-compact">
  World Diffusion
</div> -->

<div style="display: flex; gap: 20px; margin-bottom: 2em;">
  <img src="/assets/HillsbradDiffusion/morph_15fps.gif" alt="Project 2" style="width: 256px; object-fit: cover;">
  <div>
    <p><strong>Hillsbrad Diffusion: A World Diffusion Model Criminally Undertrained</strong><br> A qualitative look at a world diffusion model undertrained on two hours of sparse exploration of a large map.</p>
    <p>
      <a href="https://samgijsen.github.io/general/2025/01/27/HillsbradDiffusion">Blog post</a> 
      <!-- <a href="https://github.com/SamGijsen/HillsbradDiffusion">Code</a> -->
    </p>
  </div>
</div>

## Some Previous Work
<hr style="margin: 0.5em 0;">

<div class="title-compact">
  Neural surprise in somatosensory Bayesian learning
  <span>Sam Gijsen, Miro Grundei, Robert T. Lange, Dirk Ostwald, Felix Blankenburg</span>
</div>
<div style="display: flex; gap: 20px; margin-bottom: 2em;">
  <img src="/assets/papers/neural_surprise.png" alt="Project 2" style="width: 400px; object-fit: cover;">
  <div>
    <p>Computational modeling of neural signals using information-theoretic measures shows perceptual learning can be described as a process of probabilistic inference.</p>
    <p>
      <a href="https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1008068">PLOS Computational Biology</a> • 
      <a href="https://github.com/SamGijsen/SurpriseInSomesthesis">Code</a> 
    </p>
  </div>
</div>

<hr style="margin: 0.5em 0;">

<div class="title-compact">
  Active inference and the two-step task
  <span>Sam Gijsen, Miro Grundei, Felix Blankenburg</span>
</div>
<div style="display: flex; gap: 20px; margin-bottom: 2em;">
  <img src="/assets/papers/twostep.png" alt="Project 2" style="width: 300px; object-fit: cover;">
  <div>
    <p>Compared to reinforcement learning, active inference models can better describe human sequential decision-making using probablistic surprise minimization.</p>
    <p>
      <a href="https://www.nature.com/articles/s41598-022-21766-4">Scientific Reports</a> • 
      <a href="https://github.com/SamGijsen/AI2step">Code</a> 
    </p>
  </div>
</div>

<hr style="margin: 0.5em 0;">

