# 🎨 X-Omni: Reinforcement Learning Makes Autoregressive Image Generative Models Great Again

<p align="center">
  <a href="https://x-omni-team.github.io/">🏠 Project Page</a> |
  <a href="">📄 Paper</a> |
  <a href="">🤗 HuggingFace Model</a> |
  <a href="">🚀 HuggingFace Space</a> |
  <a href="#my-benchmark-section">📊 LongText-Bench</a>
</p>


Official inference code and LongText-Bench benchmark for our paper **X-Omni**, a unified discrete autoregressive model for both image and language modalities.

## 🌟 Highlights

- **Unified Modeling Approach**: A discrete autoregressive model handling image and language modalities.
- **Superior Instruction Following**: Exceptional capability to follow complex instructions.
- **Superior Text Rendering**: Accurately render text in multiple languages, including both English and Chinese.
- **Arbitrary resolutions**: Produces aesthetically pleasing images at arbitrary resolutions.

## 🚀 Quick Start Guide

### Installation
```bash
conda create -n xomni python==3.12
conda activate xomni
pip install -r requirements
pip install flash-attn --no-build-isolation 
```
If you get trouble in installing flash_attn, please refer to the offical repository: https://github.com/Dao-AILab/flash-attention. We recommand installing from .whl file like:
```bash
pip install flash_attn-2.7.3+cu12torch2.6cxx11abiFALSE-cp312-cp312-linux_x86_64.whl
```
### Inference
#### 1. Image Generation in English
```bash
POPMRT="Input your prompt here"
IMG_PATH=/path/to/save/generation
FLUX_PATH=/path/to/FLUX.1-dev
python generate.py \
    --model_name_or_path X-Omni/X-Omni-En \
    --flux_model_name_or_path $FLUX_PATH \
    --prompt $PROMPT \
    --image-size 1152 1152 \
    --cfg-scale 1.0 \
    --min-p 0.03 \
    --output-path $IMG_PATH
```

#### 2. Image Generation in Chinese
```bash
PROMPT="请输入你的提示词"
IMG_PATH=/path/to/save/generation
FLUX_PATH=/path/to/FLUX.1-dev
python generate.py \
    --model_path X-Omni/X-Omni-Zh \
    --flux_model_name_or_path $FLUX_PATH \
    --prompt $PROMPT \
    --image-size 1152 1152 \
    --cfg-scale 1.0 \
    --min-p 0.03 \
    --output-path $IMG_PATH
```

#### 3. Multi-modal Chat
```bash
IMG_PATH=/path/to/your/input/image
PROMPT="Input your question here"
FLUX_PATH=/path/to/FLUX.1-dev
python chat.py \
    --model_name_or_path X-Omni/X-Omni-En \
    --flux_model_name_or_path $FLUX_PATH \
    --prompt $PROMPT \
    --image-path $IMG_PATH
```

<a id="my-benchmark-section"></a>
## 📊 LongText-Bench
### 1. Install environment for Qwen2.5-VL
```bash
pip install transformers==4.52.0
pip install qwen_vl_utils
```
### 2. Sample results
Generate images according to prompts in 'text_prompts.jsonl' and 'text_prompts_zh.jsonl' and save according to the following structure:
```
├── <SAMPLE_DIR>/
│   ├── 0000_1.png
│   ├── 0000_2.png
│   ├── 0000_3.png
│   ├── 0000_4.png
│   ├── ...
│   ├── 0199_1.png
│   ├── 0199_2.png
│   ├── 0199_3.png
│   └── 0199_4.png
```
Make sure your generation results saved in the format: {prompt_id}_{repeat_id}.png, where prompt_id is provided in the prompt file and we uniformly sample each prompt four times to calculate the final results.
### 3. Evaluation
Here we provide a distributed evaluation script with torch DDP:
```bash
cd textbench
bash eval.sh
```
Replace MODE and SAMPLE_FOLDER in this script according to your generation results in step2. Feel free to modify the related parameters according to your requirements. 
## 📖 Citation

If you find this project helpful for your research or use it in your own work, please cite our paper:
```bibtex
@article{geng2025xomni,
      author       = {Zigang Geng, Yibing Wang, Yeyao Ma, Chen Li, Yongming Rao, Shuyang Gu, Zhao Zhong, Qinglin Lu, Han Hu, Xiaosong Zhang, Linus, Di Wang and Jie Jiang},
      title        = {X-Omni: Reinforcement Learning Makes Autoregressive Image Generative Models Great Again},
      journal      = {CoRR},
      volume       = {abs/None},
      year         = {2025},
}
```

---

## 📬 Contact & Feedback

For questions or feedback, please don't hesitate to reach out:

- **Yibing Wang**: wangyibing18@mails.ucas.ac.cn
- **Tencent Hunyuan X Team**

---

⭐️ If this repository helped your research, please star 🌟 this repo 👍!
