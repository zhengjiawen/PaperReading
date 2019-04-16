# EdgeBoxes Class

### Parameter

 

| parameter          | comments                   | Note                                            |
| ------------------ | -------------------------- | ----------------------------------------------- |
| Alpha              | 滑动窗口步长               | step size of sliding window search              |
| Beta               | object proposals的nms 阈值 | nms threshold for object proposals              |
| minScore           |                            | min score of boxes to detect                    |
| maxBoxes           |                            | max number of boxes to detect                   |
| Eta                |                            | adaptation rate for nms threshold (see arXiv15) |
| 下面的参数可以忽略 |                            |                                                 |
| maxAspectRatio     |                            | max aspect ratio of boxes                       |
| minBoxArea         |                            | minimum area of boxes                           |
| gamma              | 方程一中的r                | affinity sensitivity                            |
| EdgeMergeThreshold | 小于此阈值的EdgeGroup合并  | increase to trade off accuracy for speed        |
| Kappa              | 尺度灵敏度，hb公式中的k    | scale sensitivity, see equation 3 in paper      |
| clusterMinMag      |                            | adaptation rate for nms threshold               |
|                    |                            |                                                 |

