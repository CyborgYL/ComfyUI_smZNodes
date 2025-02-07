
# smZNodes
A selection of custom nodes for [ComfyUI](https://github.com/comfyanonymous/ComfyUI).

1. [CLIP Text Encode++](#clip-text-encode)
2. [Settings](#settings)

## CLIP Text Encode++

<p align="center">
    <div class="row">
        <p align="center">
            <img width="1255" alt="Clip Text Encode++ – Default settings on stable-diffusion-webui" src="https://github.com/shiimizu/ComfyUI_smZNodes/assets/54494639/ec85fd20-2b83-43cd-9f19-5aba34034e2a">
    </div>
</p>





CLIP Text Encode++ can generate identical embeddings from [stable-diffusion-webui](https://github.com/AUTOMATIC1111/stable-diffusion-webui) for [ComfyUI](https://github.com/comfyanonymous/ComfyUI).


This means you can reproduce the same images generated from `stable-diffusion-webui` on `ComfyUI`.

Simple prompts generate _identical_ images. More complex prompts with complex attention/emphasis/weighting may generate images with slight differences due to how `ComfyUI` denoises images. In that case, you can enable the option to use another denoiser with the Settings node.


### Features

- [Prompt editing](https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Features#prompt-editing)
    - [Alternating words](https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Features#alternating-words)
- Weight normalization
- Usage of `BREAK` and `AND` keywords
- Optional `embedding:` identifier

### Installation

Three methods are available for installation:

1. Load via [ComfyUI Manager](https://github.com/ltdrdata/ComfyUI-Manager)
2. Clone the repository directly into the extensions directory.
3. Download the project manually.


#### Load via ComfyUI Manager


<div align="center">
    <img width="1207" alt="ComfyUI Manager" src="https://github.com/shiimizu/ComfyUI_smZNodes/assets/54494639/310d934d-c8db-4c4a-af2a-7a26938eb751">
    <p>Install via ComfyUI Manager</p>
</div>

#### Clone Repository

```shell
cd path/to/your/ComfyUI/custom_nodes
git clone https://github.com/shiimizu/ComfyUI_smZNodes.git
```

#### Download Manually

1. Download the project archive from [here](https://github.com/shiimizu/ComfyUI_smZNodes/archive/refs/heads/main.zip).
2. Extract the downloaded zip file.
3. Move the extracted files to `path/to/your/ComfyUI/custom_nodes`.
4. Restart ComfyUI

The folder structure should resemble: `path/to/your/ComfyUI/custom_nodes/ComfyUI_smZNodes`.


### Update

To update the extension, update via [ComfyUI Manager](https://github.com/ltdrdata/ComfyUI-Manager) or pull the latest changes from the repository:

```shell
cd path/to/your/ComfyUI/custom_nodes/ComfyUI_smZNodes
git pull
```

### Comparisons
These images can be dragged into ComfyUI to load their workflows. Each image is done using the [Silicon29](https://huggingface.co/Xynon/SD-Silicon) (in SD v1.5) checkpoint with 18 steps using the Heun sampler.

|stable-diffusion-webui|A1111 parser|Comfy parser|
|:---:|:---:|:---:|
| ![00008-0-cinematic wide shot of the ocean, beach, (palmtrees_1 5), at sunset, milkyway](https://github.com/shiimizu/ComfyUI_smZNodes/assets/54494639/719457d8-96fc-495e-aabc-48c4fe4d648d) | ![A1111 parser comparison 1](https://github.com/shiimizu/ComfyUI_smZNodes/assets/54494639/c7e0d3cd-ae22-4a6a-bc21-a2b6e10f9652) | ![Comfy parser comparison 1](https://github.com/shiimizu/ComfyUI_smZNodes/assets/54494639/21415ca1-57f9-454a-8e63-19b04832a38c) |
| ![00007-0-a photo of an astronaut riding a horse on mars, ((palmtrees_1 2) on water)](https://github.com/shiimizu/ComfyUI_smZNodes/assets/54494639/9ad8b569-8c6d-4a09-bf36-288d81ce4cf9) | ![A1111 parser comparison 2](https://github.com/shiimizu/ComfyUI_smZNodes/assets/54494639/6986be92-b210-4fdd-8667-7004d6cd628c) | ![Comfy parser comparison 2](https://github.com/shiimizu/ComfyUI_smZNodes/assets/54494639/c0d918bb-32df-4aaa-ae85-def22c2d7d07) |

Image slider links:
- https://imgsli.com/MTkxMjE0
- https://imgsli.com/MTkxMjEy

### Options

|Name|Description|
| --- | --- |
| `parser` | The parser selected to parse prompts into tokens and then transformed (encoded) into embeddings. Taken from [`automatic`](https://github.com/vladmandic/automatic/discussions/99#discussioncomment-5931014). |
| `mean_normalization` | Whether to take the mean of your prompt weights. It's `true` by default on `stable-diffusion-webui`.<br>This is implemented according to `stable-diffusion-webui`. (They say that it's probably not the correct way to take the mean.) |
| `multi_conditioning` | This is usually set to `true` for your positive prompt and `false` for your negative prompt. <blockquote> For each prompt, the list is obtained by splitting the prompt using the `AND` separator. <br>See [Compositional Visual Generation with Composable Diffusion Models](https://energy-based-model.github.io/Compositional-Visual-Generation-with-Composable-Diffusion-Models/) </blockquote> |
|`use_old_emphasis_implementation`| <blockquote>Use old emphasis implementation. Can be useful to reproduce old seeds.</blockquote>|

> [!IMPORTANT]  
> You can right click the node to show/hide some of the widgets. E.g. the `with_SDXL` option.

<br>

| Parser            | Description                                                                      |
| ----------------- | -------------------------------------------------------------------------------- |
| `comfy`           | The default way `ComfyUI` handles everything                                     |
| `comfy++`         | Uses `ComfyUI`'s parser but encodes tokens the way `stable-diffusion-webui` does, allowing to take the mean as they do. |
| `A1111`           | The default parser used in `stable-diffusion-webui`                              |
| `full`            | Same as `A1111` but whitespaces and newlines are stripped                        |
| `compel`          | Uses [`compel`](https://github.com/damian0815/compel)                            |
| `fixed attention` | Prompt is untampered with                                                        |

> **Note**  
> Every `parser` except `comfy` uses `stable-diffusion-webui`'s encoding pipeline.

> **Warning**  
> LoRA syntax (`<lora:name:1.0>`) is not suppprted.

## Settings

<div align="center">
    <img width="2753" alt="Settings Workflow" src="https://github.com/shiimizu/ComfyUI_smZNodes/assets/54494639/31427491-f313-4fa4-be7e-18333cba4de6">
    <p>Settings node workflow</p>
</div>


The Settings node can be used to finetune results from CLIP Text Encode++. Some settings apply globally, or just during tokenization, or just for CFGDenoiser. The `RNG` setting applies globally.

This node can change whenever it is updated, so you may have to recreate the node to prevent issues. Hook it up before CLIP Text Encode++ nodes to apply any changes. Settings can be overridden by using another Settings node somewhere past a previous one. Right click the node for the `Hide/show all descriptions` menu option.


## Tips to get reproducible results on both UIs
- Use the same seed, sampler settings, RNG (CPU or GPU), clip skip (CLIP Set Last Layer), etc.
- Ancestral samplers may not be deterministic.
- If you're using `DDIM` as your sampler, use the `ddim_uniform` scheduler.
- There are different `unipc` configurations. Adjust accordingly on both UIs.

### FAQs
- How does this differ from [`ComfyUI_ADV_CLIP_emb`](https://github.com/BlenderNeko/ComfyUI_ADV_CLIP_emb)?
    - In regards to `stable-diffusion-webui`:
      - Mine parses prompts using their parser.
      -  Mine takes the mean exactly as they do. `ComfyUI_ADV_CLIP_emb` probably takes the correct mean but hey, this is for the purpose of reproducible images.
- Where can I learn more about how ComfyUI interprets weights?
    - https://comfyanonymous.github.io/ComfyUI_examples/faq/
    - https://blenderneko.github.io/ComfyUI-docs/Interface/Textprompts/
