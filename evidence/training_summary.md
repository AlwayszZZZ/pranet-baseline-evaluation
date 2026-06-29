# Training Summary

This file summarises the self-training run used as evidence for the June-stage PraNet baseline reproduction.

## Purpose

The goal of this run was to train PraNet with the original PraNet-style training pipeline and obtain a self-trained checkpoint for baseline evaluation.

## Model and data

| Item | Value |
| --- | --- |
| Model | PraNet |
| Backbone | Res2Net |
| Training data | PraNet training dataset under `./data/TrainDataset` |
| Self-trained model name | `PraNet_Res2Net_20260622` |
| Final evaluated checkpoint | `PraNet_Res2Net_20260622/PraNet-19.pth` |

## Environment

| Item | Value |
| --- | --- |
| Host | `ThinkStation-P920-06` |
| Working directory | `/home/scxml4/projects/PraNet0607-1` |
| Conda environment | `pranet` |
| Python | `3.9.25` |
| PyTorch | `1.13.1` |
| Torch CUDA | `11.7` |
| GPU | NVIDIA RTX A5000 |

## Training setup

| Item | Value |
| --- | --- |
| Epoch setting | 20 |
| Batch size | 16 |
| Input size | 352 |
| Training save name | `PraNet_Res2Net_20260622` |

## Training command

```bash
python MyTrain.py --epoch 20 --batchsize 16 --trainsize 352 --train_path ./data/TrainDataset --train_save PraNet_Res2Net_20260622
```

## Training output

The run produced the following checkpoints:

| Checkpoint | File size | Usage |
| --- | ---: | --- |
| `PraNet_Res2Net_20260622/PraNet-9.pth` | 130,765,289 bytes | intermediate checkpoint |
| `PraNet_Res2Net_20260622/PraNet-19.pth` | 130,766,213 bytes | final checkpoint used for evaluation |

The original PraNet training loop saves the final checkpoint as `PraNet-19.pth` when the epoch setting is 20. Therefore, `PraNet-19.pth` is treated as the final self-trained checkpoint in this run.

## Checkpoint identity

```text
Remote checkpoint path:
~/projects/PraNet0607-1/snapshots/PraNet_Res2Net_20260622/PraNet-19.pth

SHA256:
76c16089d589985618ff08c132c805b047ce62d2a1dc469cf07ee032a62753ee
```

The checkpoint file is not included in this repository because it is a large model artifact. The hash is recorded to identify the exact evaluated file.

## Source evidence on workstation

The complete working records remain on the remote workstation and will be organised separately. Relevant records include the training log, environment and command record, checkpoint listing, and checksum record.

## Interpretation

This training run confirms that the PraNet training pipeline was executed successfully and produced a usable self-trained checkpoint for subsequent official MATLAB evaluation.
