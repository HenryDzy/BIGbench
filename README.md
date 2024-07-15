# BIGbench: A Unified Benchmark for Social Bias in Text-to-Image Models Based on Multi-modal LLM
This repository is supplement material for the paper: BIGbench: A Unified Benchmark for Social Bias in Text-to-Image Models Based on Multi-modal LLM

🛰️: [![Toyset](https://img.shields.io/badge/Project-Toyset-87CEEB)]() &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;
📖: [![paper](https://img.shields.io/badge/arXiv-Paper-<COLOR>.svg)]() &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;

## 📚 Features
* Clear and robust definition. We compiled and refined existing definitions of bias in T2I models into a comprehensive framework that effectively distinguishes and assesses various types of biases.

* Large prompt dataset. Our BIGbench consists of a dataset with 2654 prompts, which includes 1969 occupations-related prompt, 264 characteristics-related prompts and 421 social-relations-related prompts.
<p align="center">
  <img src="Figure/fig4.png" width="75%"/>
</p>

* Multi-dimensional evaluation metric. Our evaluation metrics for generative bias cover six dimensions, four levels and the manifestation factor $`\eta`$ for each model.
<p align="center">
  <img src="Figure/fig6.png" width="35%"/> <img src="Figure/fig3.png" width="75%"/>
</p>

## 📊 Test Models
* [Stable Cascade](https://huggingface.co/stabilityai/stable-cascade)
* [StableDifussion XL](https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0)
* [StableDifussion XL Turbo](https://huggingface.co/stabilityai/sdxl-turbo)
* [StableDifussion XL Lightning](https://huggingface.co/ByteDance/SDXL-Lightning)
* [PixArt Sigma](https://github.com/PixArt-alpha/PixArt-sigma)

## 📈 Quantitive Result:
For each prompt, we generate at least 400 images on each T2I model we chose. Based on the generating speed, some models even have 800 images for each prompt (e.g. sdxl Turbo).
<p align="center">
  <img src="Figure/fig1.png" width="90%"/>
</p>
We used our algorithm to evaluate each T2I model we chose and calculate the implicit bias, explicit bias and the manifestation factor. The result is shown in the following figure:
<p align="center">
  <img src="Figure/total.png" width="90%"/>
</p>

## 📌 Prerequesties
1. `conda create -n bigbench python=3.11`
2. `pip install -r requirements.txt`
3. download InternViT and put it into `./model`

## 🌟 Usage!
* First, download InternViT model, put it into `./model`.
* Second, change `model`in `1_generate.py` to the path you store your model workflow json file. Usually, your workflow should be stored under `./data/workflow`. Change the port of `ip` in`1_generate.py` to the port of your own Comfyui and run Comfyui independently. Then, you may run `1_generate.py` to generate images based on our prompt set. 
* Third, change `model` in  `2_align.py` to the name of T2I model you use. Change `source_path` to the path where you store the images generated by `1_generate.py`. Then, you may run `2_align.py` to align texts and images through InternViT.
* Fourth, change `model` in  `3_evaluate.py` to the name of T2I model you use. Change `align_path` to the path of the json file generated by `2_align.py`. Then, you may run `3_evaluate.py` to generate th final result.
