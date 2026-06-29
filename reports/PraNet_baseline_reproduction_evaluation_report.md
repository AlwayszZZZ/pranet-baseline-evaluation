# PraNet Baseline Reproduction and Evaluation Report

## 1. Purpose

This report summarises the June-stage PraNet baseline reproduction and evaluation work for the dissertation project **Cross-Dataset Generalisation for Robust Polyp Segmentation**.

The purpose of this work was to verify that the PraNet baseline could be trained and evaluated locally, and to establish a reliable evaluation pipeline for later cross-dataset generalisation analysis.

This report focuses on PraNet. Polyp-PVT and HarDNet-MSEG were reviewed as related baseline architectures, but they were not re-trained or re-evaluated in this repository.

## 2. Scope

The completed work includes:

1. Training a self-trained PraNet checkpoint using the PraNet training pipeline.
2. Evaluating the official PraNet checkpoint and the self-trained checkpoint with the official MATLAB evaluation protocol.
3. Comparing the local re-evaluation of the official checkpoint with the published PraNet paper results.
4. Summarising the cross-dataset performance pattern as preparation for the next research stage.

This report should not be interpreted as a full reproduction of every table, ablation study, and visual comparison in the original PraNet paper.

## 3. Training Reproduction

The self-trained checkpoint was produced on the remote workstation using the following training configuration.

| Item | Value |
| --- | --- |
| Model | PraNet |
| Backbone | Res2Net |
| Epoch setting | 20 |
| Batch size | 16 |
| Input size | 352 |
| Training data path | `./data/TrainDataset` |
| Training save name | `PraNet_Res2Net_20260622` |
| Final evaluated checkpoint | `PraNet_Res2Net_20260622/PraNet-19.pth` |

Training command:

```bash
python MyTrain.py --epoch 20 --batchsize 16 --trainsize 352 --train_path ./data/TrainDataset --train_save PraNet_Res2Net_20260622
```

The final self-trained checkpoint is identified as:

```text
Remote checkpoint path:
~/projects/PraNet0607-1/snapshots/PraNet_Res2Net_20260622/PraNet-19.pth

SHA256:
76c16089d589985618ff08c132c805b047ce62d2a1dc469cf07ee032a62753ee
```

More training details are recorded in `evidence/training_summary.md`.

## 4. Evaluation Protocol

The final reported results are based on the official MATLAB evaluation toolbox from the PraNet project.

Earlier lightweight Python evaluation was used only as a preliminary sanity check and is not used as final evidence in this report.

Two checkpoints were evaluated:

| Model name in results | Meaning |
| --- | --- |
| `PraNet` | Official PraNet checkpoint |
| `PraNet_Res2Net_20260622` | Self-trained PraNet checkpoint |

The evaluation was conducted on five standard PraNet test datasets:

| Dataset | Images | Description |
| --- | ---: | --- |
| CVC-300 | 60 | EndoScene / CVC-T test subset |
| CVC-ClinicDB | 62 | CVC-612 test subset |
| Kvasir | 100 | Kvasir-SEG test subset |
| CVC-ColonDB | 380 | cross-dataset test set |
| ETIS-LaribPolypDB | 196 | cross-dataset test set |

The main metrics reported here are mean Dice, mean IoU, weighted F-measure, S-measure, mean E-measure, and MAE. The complete MATLAB result table is provided in `evidence/matlab_summary.md`.

## 5. MATLAB Evaluation Results

The following table shows the main MATLAB evaluation results for the official PraNet checkpoint and the self-trained checkpoint.

| Dataset | Images | Model | meanDic | meanIoU | wFm | Sm | meanEm | MAE |
| --- | ---: | --- | ---: | ---: | ---: | ---: | ---: | ---: |
| CVC-300 | 60 | PraNet | 0.870457 | 0.796006 | 0.843210 | 0.925425 | 0.949669 | 0.009863 |
| CVC-300 | 60 | PraNet_Res2Net_20260622 | 0.878459 | 0.805805 | 0.851000 | 0.928175 | 0.955604 | 0.008747 |
| CVC-ClinicDB | 62 | PraNet | 0.898308 | 0.848239 | 0.896248 | 0.936104 | 0.962138 | 0.009354 |
| CVC-ClinicDB | 62 | PraNet_Res2Net_20260622 | 0.914265 | 0.862630 | 0.910597 | 0.940143 | 0.968714 | 0.009527 |
| Kvasir | 100 | PraNet | 0.893839 | 0.835452 | 0.880041 | 0.912484 | 0.939939 | 0.030416 |
| Kvasir | 100 | PraNet_Res2Net_20260622 | 0.896112 | 0.842618 | 0.886348 | 0.914973 | 0.941366 | 0.027578 |
| CVC-ColonDB | 380 | PraNet | 0.710777 | 0.639350 | 0.698603 | 0.820221 | 0.846401 | 0.042926 |
| CVC-ColonDB | 380 | PraNet_Res2Net_20260622 | 0.746260 | 0.667907 | 0.727682 | 0.836270 | 0.868881 | 0.036387 |
| ETIS-LaribPolypDB | 196 | PraNet | 0.627555 | 0.565739 | 0.600759 | 0.793297 | 0.807621 | 0.030750 |
| ETIS-LaribPolypDB | 196 | PraNet_Res2Net_20260622 | 0.648443 | 0.584684 | 0.617012 | 0.802088 | 0.823030 | 0.027702 |

## 6. Comparison with Published PraNet Results

To check whether the local evaluation pipeline is reliable, the official PraNet checkpoint was re-evaluated locally and compared with the published PraNet paper results. Published values are rounded as reported in the paper.

| Dataset | Published meanDic | Local official meanDic | Published meanIoU | Local official meanIoU | Published MAE | Local official MAE |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| Kvasir | 0.898 | 0.893839 | 0.840 | 0.835452 | 0.030 | 0.030416 |
| CVC-ClinicDB / CVC-612 | 0.899 | 0.898308 | 0.849 | 0.848239 | 0.009 | 0.009354 |
| CVC-ColonDB | 0.709 | 0.710777 | 0.640 | 0.639350 | 0.045 | 0.042926 |
| ETIS-LaribPolypDB | 0.628 | 0.627555 | 0.567 | 0.565739 | 0.031 | 0.030750 |
| CVC-300 / CVC-T | 0.871 | 0.870457 | 0.797 | 0.796006 | 0.010 | 0.009863 |

The local official-checkpoint results are close to the published values. This supports the reliability of the local MATLAB evaluation pipeline. Small numerical differences may come from implementation details such as image resizing, prediction-map saving, interpolation settings, MATLAB/library versions, or dataset package details.

## 7. Observations

The self-trained checkpoint produced valid PraNet segmentation results across all five datasets. It performs well on Kvasir, CVC-ClinicDB, and CVC-300, and obtains higher mean Dice and mean IoU than the locally re-evaluated official checkpoint on all five datasets in this evaluation run.

The results also show a clear cross-dataset performance drop. Both the official checkpoint and the self-trained checkpoint perform much lower on CVC-ColonDB and ETIS-LaribPolypDB than on Kvasir and CVC-ClinicDB. This pattern is consistent with the motivation of the dissertation project: models trained on one or several datasets may degrade on unseen datasets because of domain shift.

## 8. Limitations

This stage mainly focuses on quantitative evaluation. It does not yet include systematic visual comparison, failure-case categorisation, or detailed analysis of small polyps, low-contrast regions, boundary ambiguity, colour distribution changes, and other domain-shift factors.

The current repository also does not include large artifacts such as datasets, prediction masks, model weights, or `.mat` files. These artifacts are kept outside this clean submission repository.

## 9. Next Step

The next stage should extend this baseline evaluation into cross-dataset analysis. The most important follow-up tasks are:

1. collect visual examples from successful and failed cases;
2. compare performance across seen-style and unseen datasets;
3. analyse possible causes of degradation, including low contrast, boundary ambiguity, small objects, reflections, and colour distribution shift;
4. use these findings to motivate domain adaptation or domain generalisation methods.

## 10. Evidence Index

Supporting files in this repository:

```text
evidence/training_summary.md
evidence/evaluation_summary.md
evidence/matlab_summary.md
```

Raw material and logs are kept in the material repository:

```text
https://github.com/AlwayszZZZ/codex-pranet-baseline-reproduction
```
