# PraNet Baseline Reproduction and Evaluation Report

## 1. Purpose of the Report

This report summarises the completion of the PraNet baseline reproduction and evaluation work. Following the training procedure of PraNet, a self-trained checkpoint was obtained. Both the official PraNet weights and the self-trained weights were then tested and evaluated.

## 2. Evaluation Settings

The main parameters used in the training command were as follows: the number of epochs was set to 20, the batch size was 16, the input size was 352, and the training snapshot directory was `PraNet_Res2Net_20260622`.

The evaluation was conducted on the five test datasets provided in the PraNet project:

| Dataset           | Images | Description                                            |
| ----------------- | -----: | ------------------------------------------------------ |
| CVC-300           |     60 | Corresponds to CVC-T / EndoScene test set in the paper |
| CVC-ClinicDB      |     62 | Test subset of CVC-612                                 |
| Kvasir            |    100 | Kvasir-SEG test set                                    |
| CVC-ColonDB       |    380 | Cross-dataset test set                                 |
| ETIS-LaribPolypDB |    196 | Cross-dataset test set                                 |

The evaluation was performed using the MATLAB evaluation toolbox. The main metrics include mean Dice, mean IoU, weighted F-measure, S-measure, mean E-measure, and MAE.

## 3. Evaluation Results of PraNet Weights

The table below shows the main evaluation results of the official PraNet weights and the self-trained weights on the five test datasets.

| Dataset           | Images | Model                   |  meanDic |  meanIoU |      wFm |       Sm |   meanEm |      MAE |
| ----------------- | -----: | ----------------------- | -------: | -------: | -------: | -------: | -------: | -------: |
| CVC-300           |     60 | PraNet                  | 0.870457 | 0.796006 | 0.843210 | 0.925425 | 0.949669 | 0.009863 |
| CVC-300           |     60 | PraNet_Res2Net_20260622 | 0.878459 | 0.805805 | 0.851000 | 0.928175 | 0.955604 | 0.008747 |
| CVC-ClinicDB      |     62 | PraNet                  | 0.898308 | 0.848239 | 0.896248 | 0.936104 | 0.962138 | 0.009354 |
| CVC-ClinicDB      |     62 | PraNet_Res2Net_20260622 | 0.914265 | 0.862630 | 0.910597 | 0.940143 | 0.968714 | 0.009527 |
| Kvasir            |    100 | PraNet                  | 0.893839 | 0.835452 | 0.880041 | 0.912484 | 0.939939 | 0.030416 |
| Kvasir            |    100 | PraNet_Res2Net_20260622 | 0.896112 | 0.842618 | 0.886348 | 0.914973 | 0.941366 | 0.027578 |
| CVC-ColonDB       |    380 | PraNet                  | 0.710777 | 0.639350 | 0.698603 | 0.820221 | 0.846401 | 0.042926 |
| CVC-ColonDB       |    380 | PraNet_Res2Net_20260622 | 0.746260 | 0.667907 | 0.727682 | 0.836270 | 0.868881 | 0.036387 |
| ETIS-LaribPolypDB |    196 | PraNet                  | 0.627555 | 0.565739 | 0.600759 | 0.793297 | 0.807621 | 0.030750 |
| ETIS-LaribPolypDB |    196 | PraNet_Res2Net_20260622 | 0.648443 | 0.584684 | 0.617012 | 0.802088 | 0.823030 | 0.027702 |

The results show that PraNet performs well on Kvasir, CVC-ClinicDB, and CVC-300, but its scores decrease noticeably on CVC-ColonDB and ETIS-LaribPolypDB, indicating that its generalisation ability still needs improvement. In this local evaluation run, the self-trained checkpoint achieved comparable or slightly higher mean Dice and mean IoU scores than the locally re-evaluated official checkpoint. This indicates that the training process produced a valid and usable PraNet checkpoint, rather than serving as a claim of superiority over the original PraNet model.

## 4. Comparison with the Results Reported in the PraNet Paper

To verify the reliability of the local evaluation pipeline, this report compares the re-evaluation results of the official PraNet weights with the published results reported in the PraNet paper.

| Dataset                | Published meanDic | My official meanDic | Published meanIoU | My official meanIoU | Published MAE | My official MAE |
| ---------------------- | ----------------: | ------------------: | ----------------: | ------------------: | ------------: | --------------: |
| Kvasir                 |             0.898 |            0.893839 |             0.840 |            0.835452 |         0.030 |        0.030416 |
| CVC-ClinicDB / CVC-612 |             0.899 |            0.898308 |             0.849 |            0.848239 |         0.009 |        0.009354 |
| CVC-ColonDB            |             0.709 |            0.710777 |             0.640 |            0.639350 |         0.045 |        0.042926 |
| ETIS-LaribPolypDB      |             0.628 |            0.627555 |             0.567 |            0.565739 |         0.031 |        0.030750 |
| CVC-300 / CVC-T        |             0.871 |            0.870457 |             0.797 |            0.796006 |         0.010 |        0.009863 |

The results obtained by re-evaluating the official weights are generally consistent with the values reported in the paper. Minor numerical differences may be caused by implementation details such as image resizing, prediction map saving, MATLAB/Python/library versions, interpolation methods, or dataset package differences.

## 5. Summary

In this stage, the local training and evaluation of PraNet were completed. The evaluation results are generally consistent with the published results in the PraNet paper. The results also show a clear performance drop on cross-dataset test sets, indicating that cross-dataset generalisation remains a key challenge.

This report mainly focuses on quantitative metrics. Visual comparison and failure case analysis have not yet been systematically included. In the next stage, visual results should be further analysed to investigate how small polyps, low-contrast regions, and boundary ambiguity affect model performance.

## 6. Reproducibility Notes

The self-trained checkpoint used in this report is:

```text
~/projects/PraNet0607-1/snapshots/PraNet_Res2Net_20260622/PraNet-19.pth
```

SHA256:

```text
76c16089d589985618ff08c132c805b047ce62d2a1dc469cf07ee032a62753ee
```

The checkpoint file is not included in this repository because it is a large model artifact. The complete working records, including the training log, environment and command record, checkpoint listing, and checksum record, remain on the remote workstation and will be organised separately.

Key supporting files in this repository are:

* `evidence/training_summary.md`
* `evidence/evaluation_summary.md`
* `evidence/matlab_summary.md`
