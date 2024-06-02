# ComfyUI KISEKAE-OOTD

### Detectron2 プロジェクトの README.md の概要

このプロジェクトは、様々なデータセットで事前訓練されたモデルを使用して、画像やビデオからオブジェクトを検出し、セグメンテーションすることができます。

#### 主な特徴
- 複数の最先端アルゴリズムとモデルがサポートされています。
- カスタムデータセットでの訓練が可能。
- GPU および CPU での推論がサポートされています。

#### インストール方法
Detectron2 は PyTorch に基づいており、以下のコマンドでインストールできます。
```bash
pip install detectron2
```

#### 使用方法
- **モデルの訓練**: Detectron2 はコマンドラインツール `train_net.py` を提供しており、簡単にモデルの訓練が行えます。
  
```38:70:humanparsing/mhp_extension/detectron2/GETTING_STARTED.md
### Training & Evaluation in Command Line

We provide a script in "tools/{,plain_}train_net.py", that is made to train
all the configs provided in detectron2.
You may want to use it as a reference to write your own training script.

To train a model with "train_net.py", first
setup the corresponding datasets following
[datasets/README.md](./datasets/README.md),
then run:
```
cd tools/
./train_net.py --num-gpus 8 \
	--config-file ../configs/COCO-InstanceSegmentation/mask_rcnn_R_50_FPN_1x.yaml
```

The configs are made for 8-GPU training.
To train on 1 GPU, you may need to [change some parameters](https://arxiv.org/abs/1706.02677), e.g.:
```
./train_net.py \
	--config-file ../configs/COCO-InstanceSegmentation/mask_rcnn_R_50_FPN_1x.yaml \
	--num-gpus 1 SOLVER.IMS_PER_BATCH 2 SOLVER.BASE_LR 0.0025
```

For most models, CPU training is not supported.

To evaluate a model's performance, use
```
./train_net.py \
	--config-file ../configs/COCO-InstanceSegmentation/mask_rcnn_R_50_FPN_1x.yaml \
	--eval-only MODEL.WEIGHTS /path/to/checkpoint_file
```
For more options, see `./train_net.py -h`.
```

- **モデルの評価**: 訓練されたモデルの性能を評価するためのコマンドも用意されています。
  
```64:69:humanparsing/mhp_extension/detectron2/GETTING_STARTED.md
To evaluate a model's performance, use
```
./train_net.py \
	--config-file ../configs/COCO-InstanceSegmentation/mask_rcnn_R_50_FPN_1x.yaml \
	--eval-only MODEL.WEIGHTS /path/to/checkpoint_file
```
```

2024-05-30:
