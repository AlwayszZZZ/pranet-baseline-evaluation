# Training Summary

This file summarises the self-training run used as evidence for the June-stage PraNet baseline reproduction.

## Purpose

The goal of this run was to train PraNet with the official PraNet training pipeline and obtain a self-trained checkpoint for baseline evaluation.

## Model and data

- Model: PraNet
- Backbone: Res2Net
- Backbone pretraining: ImageNet-pretrained Res2Net weights
- Training data: official PraNet training dataset
- Self-trained model name used in the report: `PraNet_Res2Net_20260622`

## Training setup

| Item | Value |
| --- | --- |
| Epoch setting | 20 |
| Batch size | 16 |
| Input size | 352 |
| Training save name | `PraNet_Res2Net_20260622` |
| Final evaluated checkpoint | `PraNet_Res2Net_20260622/PraNet-19.pth` |

The original PraNet training script uses an epoch loop that saves the final checkpoint as `PraNet-19.pth` when the epoch setting is 20. Therefore, `PraNet-19.pth` is treated as the final self-trained checkpoint in this run.

## Training command

```bash
python MyTrain.py --epoch 20 --batchsize 16 --trainsize 352 --train_path ./data/TrainDataset --train_save PraNet_Res2Net_20260622
```

## Training output

The run produced the following checkpoints:

| Checkpoint | Usage |
| --- | --- |
| `PraNet_Res2Net_20260622/PraNet-9.pth` | intermediate checkpoint |
| `PraNet_Res2Net_20260622/PraNet-19.pth` | final checkpoint used for evaluation |

The final checkpoint file is not included in this repository because it is a large model file. The report and evaluation summaries refer to it by name.

## Interpretation

This training run confirms that the PraNet training pipeline was executed successfully and produced a usable self-trained checkpoint for subsequent evaluation.
