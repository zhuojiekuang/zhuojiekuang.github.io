---
layout: archive
title: "Projects"
permalink: /projects/
author_profile: true
---

## Machine Learning

---

**Diffusion and Flow Matching** \| [Website](https://viso.study) \| [Code](https://google.com)
- Implemented sampling loops, classifier-free guidance, SDEdit algorithm, visual anagrams, hybrid images for the Stability AI DeepFloyd IF model
- Trained flow matching model to do class-conditioned MNIST digit generation with UNet architecture, iterative denoising
<img src="/images/projects/diffusion-flow-matching.png" alt="desc" style="width:500px; display:block; margin-left: auto; margin-right: auto;">

**Chatbot Arena**
- Using the LMArena dataset, visualized battle distributions with Plotly and Gradio, explored confounding stylistic variables
- Built model ELO leaderboard like LMArena following Bradley-Terry model
<img src="/images/projects/chatbot-arena.png" alt="desc" style="width:500px; display:block; margin-left: auto; margin-right: auto;">

**NeRF** \| [Website](https://viso.study) \| [Code]()
- Using ~40 images from my camera, trained a NeRF model to render a 3D scene of an object with novel views
- NeRF pipeline from scratch, e.g. volume rendering, sinusoidal positional encoding, ray sampling, PSNR, visualizations with viser
<video src="/images/projects/nerf.mp4" style="width:400px; display:block; margin-left: auto; margin-right: auto;" autoplay loop muted playsinline></video>

**DNABERT**
- Trained a classification head on top of pretrained DNABERT-6 representations to perform species identification across human, dog, and chimpanzee genomes
- Implemented preprocessing pipeline using k-mer tokenization (k=6) to convert raw nucleotide sequences into compatible input tokens

**ConvNeXt Sound Classification**
- Used Torchaudio to transform .wav files from UrbanSound8K dataset to 2D spectrograms, then finetuned a ConvNeXt model for sound classification, achieving 90% accuracy
- Compared different 3 training paradigms: no pretraining, pretraining with frozen backbone, and pretraining with full finetuning

**ResNet-18** \| [Code]()
- Full ResNet-18 architecture in PyTorch reaching 70% validation accuracy on a sample of the Imagenet dataset

**Automatic Photo Mosaics** \| [Website](https://viso.study) \| [Code]
- Stitching images together to panoramas by estimating homographies, applying projective warping, and blending images with Laplacian pyramid
- Automated mosaic process using Harris corners, ANMS, and RANSAC homography estimation

**Fashion MNIST Classifier** \| [Code]
- Trained a Fashion MNIST classifier invariant to shifts, rotations, and blurs with scikit-learn

**Image Filtering** \| [Code]()
- Core image processing techniques such as convolution, image sharpening, hybrid images, and multi-resolution blending using Gaussian and Laplacian pyramids

**Autodifferentiation** \| [Code]
- Constructed computation graph of loss functions, implemented downstream gradient propagation using topological sort with Kahn's algorithm
- Implemented SGD, Momentum, and Adam optimizers
<img src="/images/projects/autodifferentiation.png" alt="desc" style="width:500px; display:block; margin-left: auto; margin-right: auto;">

**RISC-V Neural Network** \| [Code]()
- MNIST digit classifier with RISC-V Assembly

## Software Engineering

---

**Viso** \| [Website](https://viso.study) \| [Code](https://github.com/orgs/viso-study/repositories) \| [Presentation](https://x.com/i/broadcasts/1BdGYZzAQeAJX)
- Learning platform that transforms math questions into rich animated explanations
- Multi-agent pipeline with RAG research agent, tool calling, Manim-based rendering agent, and planning agents
- Won most technical project in AdventureX, Top 20 in amber.ac Hackathon

**RISV-C CPU** \| [Code]
- 2-stage pipelined CPU in Logisim implementing a subset of the RISC-V ISA

**AI Entrepreneurs at Berkeley** \| [Website](https://aientrepreneurs.org) \| [Code](https://github.com/orgs/viso-study/repositories)
- Founding member of $100M student-run AI incubator, built and maintain the website

## Fun

---

**Amateur keyboard player** \| [Recording](https://www.youtube.com/watch?v=hnmUMC_tGN8)
- Demoted from concert grand pianist to digital keyboardist in 2021
- Currently sporting a pirated setup with Garritan Yamaha CFX and various spectrograms for transcribing songs
