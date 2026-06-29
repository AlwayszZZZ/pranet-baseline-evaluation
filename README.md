# PraNet Baseline Evaluation

This repository is a cleaned submission snapshot for the June-stage PraNet baseline reproduction and evaluation.

It supports two deliverables:

- successfully trained PraNet model
- baseline evaluation report

## Repository structure

```text
reports/
  PraNet_baseline_reproduction_evaluation_report.md

evidence/
  training_summary.md
  evaluation_summary.md
  matlab_summary.md
```

## Included files

- `training_summary.md`: training setup and final self-trained checkpoint identity.
- `evaluation_summary.md`: evaluated checkpoints, test datasets, and evaluation protocol summary.
- `matlab_summary.md`: full MATLAB evaluation table used in the report.

## Excluded files

Datasets, pretrained weights, checkpoint files, prediction masks, and other large generated files are not included.

The final self-trained checkpoint used in the evaluation is:

```text
PraNet_Res2Net_20260622/PraNet-19.pth
```

## Suggested reading order

1. `reports/PraNet_baseline_reproduction_evaluation_report.md`
2. `evidence/training_summary.md`
3. `evidence/evaluation_summary.md`
4. `evidence/matlab_summary.md`
