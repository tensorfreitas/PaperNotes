# Focal Loss for Dense Object Detection

Introduces a one-stage detector RetinaNet that prevents the vast easy negatives on architectures like R-CNN, achieving fast object detection and surpassing the accuracy of all the two-stage detectors.

According to the authors, the **problem of not achieving the same AP as two-stage detectors** is due to the **class imbalance** on training phase. The proposed **focal loss eliminates this barrier**. 

The authors borrow a lot of similarities to other works namely:
- Anchors proposed by a Region Proposal Network (RPN)
- Feature Pyramids as in Feature Pyramid Nets (FPN) and Single Shot Multibox Detector (SSD)

The improvement in performance is not due to architectural improvements but to the proposed loss function.

In R-CNN-based detectors, the class imbalance is solved by a two-stage cascade (that filters most background samples) and sampling heuristics in the second phase (that maintains the balance of foreground and background samples). In the previously proposed one-stage detectors, the class imbalance is big (_10_4_-_10_5_ candidates per image, but only a few of them have objects). This imbalance makes training inefficient since most regions are easy negatives and in big proportions can harm the performance of the models. 

## Focal Loss

Binary Cross-Entropy: 

![ce](assets/ce.png)

Even examples that are **easy classified** (p > 0.5) have a **loss that is significant**. **When summed together they can overwhelm rare classes**. 

To address this it can be added a weight factor alpha ([0-1]) for each class (set as the inverse of class frequency ratio or as a hyperparameter). This extension of Cross-entropy is used as a baseline for comparing with Focal Loss. 

![alpha](assets/alpha_ce.png)

**The alpha does not differentiate between easy and hard examples.**  

To avoid the dominance of gradients from easy classified negatives they proposed the **focal loss**:

![FL](assets/FL.png)

![focal_loss](assets/focal_loss.png)

- Allows **efficient training without sampling** and harming the performance.
- Designed to **dow-weight inliers** (easy examples) such that **their contribution to the loss is small** event if the confidence is high, focuses on a sparse set of hard examples.
- With this loss:
  1. A misclassified example with small probability, the loss is not much affected. As the probability tends to 1, and the examples are down-weighted.
  2. **γ adjusts smoothly the down-weight** of easy examples.
  3. With **γ = 0**, we have the traditional **Cross-Entropy** loss.

In practice, the authors use an **α-balanced Focal Loss**, as it improves the overall metrics of the system:

![alpha_fl](assets/alpha_fl.png)

## References

- Lin, Tsung-Yi, Priya Goyal, Ross Girshick, Kaiming He, and Piotr Dollár. "Focal loss for dense object detection." In Proceedings of the IEEE international conference on computer vision, pp. 2980-2988. 2017.