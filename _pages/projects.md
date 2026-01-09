---
layout: archive
title: "Projects"
permalink: /projects/
author_profile: true
---

All code can be found in this [link](https://thinfi.com/0lbj3).

## Machine Learning

---

**Diffusion and flow matching** \| [Website]() \| [Code](https://thinfi.com/0lbj3)
- Implemented sampling loops, classifier-free guidance, SDEdit algorithm, visual anagrams, hybrid images for the Stability AI DeepFloyd IF model
- Trained flow matching model to do class-conditioned MNIST digit generation with UNet architecture, iterative denoising
<img src="/images/projects/diffusion-flow-matching.png" alt="desc" style="width:550px; display:block; margin-left: auto; margin-right: auto; margin-top: 20px;">

**Chatbot arena** \| [Code](https://thinfi.com/0lbj3)
- Using the LMArena dataset, visualized battle distributions with `plotly` and `gradio`, explored confounding stylistic variables
- Built model ELO leaderboard like LMArena following Bradley-Terry model
<img src="/images/projects/chatbot-arena.png" alt="desc" style="width:450px; display:block; margin-left: auto; margin-right: auto; margin-top: 10px; margin-bottom: -10px;">

**NeRF** \| [Website]() \| [Code](https://thinfi.com/0lbj3)
- Using 40 images from my camera, trained a NeRF model to render a 3D scene of an object with novel views
- NeRF pipeline from scratch, e.g. volume rendering, sinusoidal positional encoding, ray sampling, PSNR, visualizations with `viser`
<video src="/images/projects/nerf.mp4" style="width:300px; display:block; margin-left: auto; margin-right: auto; margin-top; 30px; margin-bottom: 30px;" autoplay loop muted playsinline></video>

**DNABERT** \| [Code](https://thinfi.com/0lbj3)
- Trained a classification head on top of pretrained DNABERT-6 representations to perform species identification across human, dog, and chimpanzee genomes
- Implemented preprocessing pipeline using k-mer tokenization (k=6) to convert raw nucleotide sequences into compatible input tokens
<img src="/images/projects/dnabert.jpeg" alt="desc" style="width:600px; display:block; margin-left: auto; margin-right: auto; margin-top: 30px; margin-bottom: 30px;">

**CLIP retrieval and captioning** \| [Code](https://thinfi.com/0lbj3)
- Performed retrieval and caption generation on Concadia dataset with CLIP embeddings
- Implemented Rational Speech Acts (RSA) e.g. literal listener, pragmatic speaker, pragmatic listener to select the most unambiguous utterance given a set of possible referents

**ConvNeXt sound classification** \| [Code](https://thinfi.com/0lbj3)
- Used Torchaudio to transform .wav files from UrbanSound8K dataset to 2D spectrograms, then finetuned a ConvNeXt model for sound classification, achieving 90% accuracy
- Compared different 3 training paradigms: no pretraining, pretraining with frozen backbone, and pretraining with full finetuning
<img src="/images/projects/urbansound8k.png" alt="desc" style="width:350px; display:block; margin-left: auto; margin-right: auto; margin-top: 30px; margin-bottom: 20px;">

**Text2SQL finetuning** \| [Code](https://thinfi.com/0lbj3)
- Finetuned GPT-2 to generate SQL queries executed against a database and compared performance with few-shot prompting using Hugging Face `transformers` library

**LLM MCQ finetuning** \| [Code](https://thinfi.com/0lbj3)
- Finetuned Qwen2.5-0.5B-Instruct using Hugging Face `transformers` and `trl` libraries to solve CS189 MCQs with 45% accuracy

**LLM tokenization and embeddings** \| [Code](https://thinfi.com/0lbj3)
- Implemented BPE tokenization, analyze Zipfian distributions, then trained a Skip-Gram model to compute embeddings using negative sampling
- Used `spaCy` to learn a linear transformation $W$ that maps two embedding spaces in different languages to perform machine translation, lemmatize and generate dependency trees of text corpus

**ResNet-18** \| [Code](https://thinfi.com/0lbj3)
- Full ResNet-18 architecture in PyTorch reaching 70% validation accuracy on a sample of the Imagenet dataset
<img src="/images/projects/resnet-18.png" alt="desc" style="width:500px; display:block; margin-left: auto; margin-right: auto; margin-top: 20px; margin-bottom: 40px;">

**Automatic photo mosaics** \| [Website]() \| [Code](https://thinfi.com/0lbj3)
- Stitching images together to panoramas by estimating homographies, applying projective warping, and blending images with Laplacian pyramid
- Automated mosaic process using Harris corners, ANMS, and RANSAC homography estimation

**Language model eval** \| [Code](https://thinfi.com/0lbj3)
- Evaluated text/audio classification, machine translation, and open-ended text generation, implemented PRC curves, Levenstein distance, BLEU score, LLM-as-a-judge

**Fashion MNIST classifier** \| [Code](https://thinfi.com/0lbj3)
- Trained a Fashion MNIST classifier invariant to shifts, rotations, and blurs with `scikit-learn`

**Image filtering** \| [Website]() \| [Code](https://thinfi.com/0lbj3)
- Core image processing techniques such as convolution, image sharpening, hybrid images, and multi-resolution blending using Gaussian and Laplacian pyramids
<img src="/images/projects/oraple.jpg" alt="desc" style="width:350px; display:block; margin-left: auto; margin-right: auto; margin-top: 20px; margin-bottom: 20px;">

**Autodifferentiation** \| [Code](https://thinfi.com/0lbj3)
- Constructed computation graph of loss functions, implemented downstream gradient propagation using topological sort with Kahn's algorithm
- Implemented SGD, Momentum, and Adam optimizers

**RISC-V MNIST classifier** \| [Code](https://thinfi.com/0lbj3)
- Fully connected neural network with RISC-V Assembly

## Software Engineering

---

**Viso** \| [Website](https://viso.study) \| [Repo](https://github.com/orgs/viso-study/repositories) \| [Presentation](https://x.com/i/broadcasts/1BdGYZzAQeAJX)
- Learning platform that transforms math questions into rich animated explanations
- Multi-agent pipeline with `smolagents` RAG research agent, tool calling, Manim rendering agent, and planning agents
- Won most technical project in AdventureX, Top 20 in amber.ac Hackathon

**RISV-C CPU** \| [Code](https://thinfi.com/0lbj3)
- 2-stage pipelined CPU in Logisim implementing a subset of the RISC-V ISA

**AI Entrepreneurs at Berkeley** \| [Website](https://aientrepreneurs.org) \| [Repo](https://github.com/AIEntrepreneursBerkeley/aientrepreneurs.org)
- Founding member of $100M student-run AI incubator, built and maintain the website

## Fun

---

**Amateur keyboard player** \| [Recordings](https://www.youtube.com/watch?v=hnmUMC_tGN8)
- Demoted from concert grand pianist to digital keyboardist
- Currently sporting a pirated setup with Garritan Yamaha CFX and various transcription tools

**Crow whispering** \| [Report]()
- Idea: expand sphere of influencing by winning command over a murder of crows
<img src="/images/projects/crows.jpg" alt="desc" style="width:350px; display:block; margin-left: auto; margin-right: auto; margin-top: 20px;">