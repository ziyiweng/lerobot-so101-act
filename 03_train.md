# Using Colab
https://colab.research.google.com/github/huggingface/notebooks/blob/main/lerobot/training-act.ipynb
## install lerobot
```bash
!git clone https://github.com/huggingface/lerobot.git
!apt-get install ffmpeg
!cd lerobot && pip install -e ".[train, dataset]"
```
## weight & biases login (optional)
```bash
!wandb login
```
## hf login
```bash
!hf auth login
```
## comment 'groot' out
```bash
!rm -rf /content/lerobot/src/lerobot/policies/groot
!pip install huggingface_hub==0.26.5 --quiet --force-reinstall
!pip install -e "/content/lerobot" --quiet
```
```bash
factory_path = "/content/lerobot/src/lerobot/policies/factory.py"


with open(factory_path, "r") as f:
   content = f.read()


# 注释 import
content = content.replace(
   "from .groot.configuration_groot import GrootConfig",
   "# from .groot.configuration_groot import GrootConfig"
)


# 防止 isinstance(..., GrootConfig) 报错
if 'GrootConfig = type("_DisabledGrootConfig", (), {})' not in content:
   content = content.replace(
       "# from .groot.configuration_groot import GrootConfig",
       """# from .groot.configuration_groot import GrootConfig
GrootConfig = type("_DisabledGrootConfig", (), {})"""
   )


with open(factory_path, "w") as f:
   f.write(content)


print("factory.py patched")
```
```bash
init_path = "/content/lerobot/src/lerobot/policies/__init__.py"


with open(init_path, "r") as f:
   content = f.read()


lines = content.split("\n")
lines = [
   "# " + line if "groot" in line.lower() and not line.strip().startswith("#")
   else line
   for line in lines
]


content = "\n".join(lines)


with open(init_path, "w") as f:
   f.write(content)


print("__init__.py patched")
```
## train
```bash
!lerobot-train \
 --dataset.repo_id=ziyiweng/act_so101_flextape_dataset \
 --policy.type=act \
 --output_dir=outputs/train/act_so101_flextape_dataset_output1 \
 --job_name=act_so101_flextape_dataset_jobname \
 --policy.device=cuda \
 --wandb.enable=True \
 --policy.repo_id=ziyiweng/act_so101_flextape_dataset_policy \
 --batch_size=8 \
 --steps=1000
```
to save steps
```bash
!lerobot-train \
 --dataset.repo_id=ziyiweng/act_so101_flextape_dataset \
 --policy.type=act \
 --output_dir=outputs/train/act_so101_flextape_dataset_output1 \
 --job_name=act_so101_flextape_dataset_jobname \
 --policy.device=cuda \
 --wandb.enable=True \
 --policy.repo_id=ziyiweng/act_so101_flextape_dataset_policy \
 --batch_size=8 \
 --steps=400 \
 --save_checkpoint=true \
 --save_freq=200
```
view saved steps
```bash
!find outputs/train/act_so101_flextape_dataset_output1
```
upload saved steps to hf
```bash
from huggingface_hub import HfApi


api = HfApi()


api.create_repo(
   repo_id="ziyiweng/act_so101_flextape_dataset_10kpolicy",
   repo_type="model",
   exist_ok=True
)
```
```bash
api.upload_folder(
   folder_path="outputs/train/act_so101_flextape_dataset_output7/checkpoints/014000/pretrained_model",
   repo_id="ziyiweng/act_so101_flextape_dataset_14kpolicy",
   repo_type="model"
)
```

