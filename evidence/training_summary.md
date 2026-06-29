# Training Summary

PraNet self-training was completed for the June-stage baseline reproduction.

## Model

- Model: PraNet with Res2Net backbone
- Self-trained model name used in the report: `PraNet_Res2Net_20260622`
- Final evaluated checkpoint: `PraNet_Res2Net_20260622/PraNet-19.pth`

## Training setup

- Epoch setting: 20
- Batch size: 16
- Input size: 352
- Training data: official PraNet training dataset

## Output

The final evaluated checkpoint is `PraNet-19.pth`. In the original PraNet training script, the epoch loop ends at epoch 19 when the epoch setting is 20, so this checkpoint is the expected final saved checkpoint for this run.
