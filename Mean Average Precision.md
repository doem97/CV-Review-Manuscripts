# Mean Average Precision
**Input** (a serial of predicted boxes with confidence, ground truth boxes) over a batch of images like this:

<img src="https://user-images.githubusercontent.com/19631039/118779193-63f0fe80-b8bd-11eb-9d4f-e52890f88912.png" width="500">

Red is predicted, Green is Ground Truth.
See also:
[COCO dataset metric](https://cocodataset.org/#detection-eval)

## Preprocessing Step:
For each image, the bounding box are get from Non Max Suppression （NMS）. It selets the outstanding box from a cluster of predicted boxes.

<img src="https://user-images.githubusercontent.com/19631039/118779513-b3372f00-b8bd-11eb-937c-e9ea53ed0264.png" width="500">

<img src="https://user-images.githubusercontent.com/19631039/118779576-c813c280-b8bd-11eb-8ffb-260e0e386de3.png" width="500">

<img src="https://user-images.githubusercontent.com/19631039/118779642-d4981b00-b8bd-11eb-8b78-28cdae97e9bd.png" width="500">

<img src="https://user-images.githubusercontent.com/19631039/118779958-2476e200-b8be-11eb-909b-04040853abfc.png" width="500">

## mAP Steps
1. For each class:
    1.  Calculate TP/FP for each predicted box, based on IoU matching with each ground truth. If can find a ground truth with IoU > **Threshold_IoU**, set as TP; else FP.
    2. Descent listing the confidence, calculate the accumulated precision and recall.
    3. AP is the Area under P-R curve.
2. Do 1-3 for each class. mAP is average among classes.

## AP@.5;.05;.95
1. Calculate mAP at 0.5, 0.05, 0.95 Threshold_IoU.
2. (AP@.5;.05;.95) = Avg(mAP(Threshold_IoU = 0.5), mAP(Threshold_IoU = 0.05), mAP(Threshold_IoU = 0.95)).

## AP50, AP75
mAP(Threshold_IoU = 0.5), mAP(Threshold_IoU = 0.75)

## AP Across Scales:
1. AP_small: AP for small objects: area < 322 
2. AP_medium: AP for medium objects: 322 < area < 962 
3. AP_large: AP for large objects: area > 962
