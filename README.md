# PraNet Baseline Evaluation

This repository is a clean June-stage deliverable for the MSc dissertation project **Cross-Dataset Generalisation for Robust Polyp Segmentation**.

It records the PraNet baseline reproduction and evaluation evidence in a compact form. The working/material repository is kept separately at:

```text
https://github.com/AlwayszZZZ/codex-pranet-baseline-reproduction
```

This repository is not intended to be a full code release. It is an evidence package showing what was trained, how it was evaluated, and what results were obtained.

## Deliverable mapping

| June deliverable item | Evidence in this repository |
| --- | --- |
| Successfully trained PraNet model | `evidence/training_summary.md` |
| Baseline evaluation report | `reports/PraNet_baseline_reproduction_evaluation_report.md` |
| Official evaluation evidence | `evidence/evaluation_summary.md`, `evidence/matlab_summary.md` |

## Main conclusion

A self-trained PraNet checkpoint was produced and evaluated using the official MATLAB evaluation protocol from the PraNet project. The official PraNet checkpoint was also re-evaluated locally. The re-evaluated official results are close to the published PraNet paper values, supporting the reliability of the local evaluation pipeline.

The self-trained checkpoint achieves valid segmentation performance across the five standard PraNet test datasets. Performance remains strong on Kvasir, CVC-ClinicDB, and CVC-300, but decreases on CVC-ColonDB and ETIS-LaribPolypDB. This cross-dataset drop supports the next project stage: analysing domain shift and cross-dataset generalisation.

## Repository structure

```text
README.md
reports/
  PraNet_baseline_reproduction_evaluation_report.md
evidence/
  training_summary.md
  evaluation_summary.md
  matlab_summary.md
```

## Main reproduced checkpoint

```text
Model name: PraNet_Res2Net_20260622
Remote checkpoint path:
~/projects/PraNet0607-1/snapshots/PraNet_Res2Net_20260622/PraNet-19.pth

SHA256:
76c16089d589985618ff08c132c805b047ce62d2a1dc469cf07ee032a62753ee
```

The checkpoint file itself is not uploaded because it is a large binary artifact. The hash records the exact evaluated model.

## Evaluation source of truth

The final reported results are based on the official MATLAB evaluation. Earlier lightweight Python evaluation was used only as a preliminary sanity check and is not used as final evidence in this repository.

The full MATLAB table is recorded in:

```text
evidence/matlab_summary.md
```

## Excluded files

Datasets, pretrained weights, checkpoint files, prediction masks, `.pth` files, `.mat` files, and other large generated artifacts are intentionally excluded.

## Suggested reading order

1. `reports/PraNet_baseline_reproduction_evaluation_report.md`
2. `evidence/training_summary.md`
3. `evidence/evaluation_summary.md`
4. `evidence/matlab_summary.md`

## Scope statement

This repository supports the June-stage PraNet baseline reproduction and evaluation. It should not be interpreted as a complete reproduction of every experiment and comparison table in the original PraNet paper. Polyp-PVT and HarDNet-MSEG are used as architectural and literature-review references elsewhere, but they are not re-trained or re-evaluated in this repository.
