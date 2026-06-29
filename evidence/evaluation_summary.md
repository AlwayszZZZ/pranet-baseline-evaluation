# Evaluation Summary

This file summarises the evaluation protocol used for the PraNet baseline reproduction.

## Evaluation method

The final reported results are based on the official MATLAB evaluation toolbox from the PraNet project.

Earlier lightweight Python evaluation was used only as a preliminary sanity check during the workflow. It is not used for the final reported metrics in this repository.

## Evaluated models

Two PraNet checkpoints were evaluated with the same MATLAB protocol:

| Model name in results | Meaning |
| --- | --- |
| `PraNet` | Official PraNet checkpoint |
| `PraNet_Res2Net_20260622` | Self-trained PraNet checkpoint from the June reproduction run |

The self-trained checkpoint is:

```text
PraNet_Res2Net_20260622/PraNet-19.pth
```

## Test datasets

The evaluation was conducted on five standard PraNet test datasets:

| Dataset | Images | Role |
| --- | ---: | --- |
| CVC-300 | 60 | EndoScene / CVC-T test subset |
| CVC-ClinicDB | 62 | CVC-612 test subset |
| Kvasir | 100 | Kvasir-SEG test subset |
| CVC-ColonDB | 380 | cross-dataset evaluation |
| ETIS-LaribPolypDB | 196 | cross-dataset evaluation |

## Metrics

The MATLAB evaluation reports the following metrics:

| Metric | Meaning |
| --- | --- |
| `meanDic` | mean Dice score |
| `meanIoU` | mean Intersection over Union |
| `wFm` | weighted F-measure |
| `Sm` | S-measure / structural similarity measure |
| `meanEm` | mean E-measure |
| `MAE` | mean absolute error |
| `maxEm` | maximum E-measure |
| `maxDice` | maximum Dice score |
| `maxIoU` | maximum IoU |
| `meanSen`, `maxSen` | mean and maximum sensitivity |
| `meanSpe`, `maxSpe` | mean and maximum specificity |

The main report focuses on `meanDic`, `meanIoU`, `wFm`, `Sm`, `meanEm`, and `MAE`.

## Result source

The complete MATLAB evaluation table is recorded in:

```text
evidence/matlab_summary.md
```

That file is treated as the source of truth for the quantitative results in the main report.

## Interpretation

The official PraNet checkpoint was re-evaluated locally. Its results are close to the published PraNet paper values, which supports the reliability of the local MATLAB evaluation pipeline.

The self-trained checkpoint was then evaluated using the same MATLAB protocol. This makes the comparison between the official checkpoint and the self-trained checkpoint consistent.

The scores on CVC-ColonDB and ETIS-LaribPolypDB are clearly lower than those on Kvasir, CVC-ClinicDB, and CVC-300. This supports the next project stage: cross-dataset generalisation analysis.
