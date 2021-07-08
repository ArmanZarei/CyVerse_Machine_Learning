<hr>

## Previous works
Point cloud is **converted to other representations** before it’s fed to a deep neural network.
<div style="text-align: center;">
    <img src="../images/previous_works.png" width=400>
</div>

## PointNet

### Tasks
- Object Classification
- Object Part Segmentation
- Semantic Scene Parsing
- ...

### Challenges 
- **Unordered** point set as input (invariant to permutations)
- Invariance under **geometric transformations**

### Permutation Invariance: Symmetric Function
$f(x_1, x_2, \cdots, x_n) \equiv f(x_{\pi_1}, x_{\pi_2}, \cdots, x_{\pi_n}), \qquad x_i \in \mathbb{R}^D$

Examples:

* $f(x_1, x_2, \cdots, x_n) = max\{x_1, x_2, \cdots, x_n\}$
* $f(x_1, x_2, \cdots, x_n) = x_1 + x_2 + \cdots + x_n$

<br>
**Observe**

$f(x_1, x_2, \cdots, x_n) = \gamma \circ g(h(x_1), \cdots, h(x_n))$ is symmetric if $g$ is symmetric

with this in mind, **vanilla PointNet** is constructed as below:
<div style="text-align: center;">
    <img src="../images/vanilla_pointNet.PNG" width=400>
</div>

which consists of:

* multi-layer perceptron (MLP)
* max pooling


### Geometric Transformations Invariance: Input Alignment by Transformer Network 
<div style="text-align: center;">
    <img src="../images/Transformer_Network.PNG" width=400>
</div>

A regularizer is also used as shown below

$L_{reg} = ||I - AA^T||_F^2$

### PointNet Classification Network
<div style="text-align: center;">
    <img src="../images/PointNet_Classification_Network.PNG">
</div>

### PointNet Segmentation Network
<div style="text-align: center;">
    <img src="../images/PointNet_Segmentation_Network.PNG">
</div>

## Resources
- [3D Point Cloud Semantic Segmentation Using Deep Learning Techniques](https://medium.com/analytics-vidhya/3d-point-cloud-semantic-segmentation-using-deep-learning-techniques-6c4504a97ce6)
- [Qi, C. R., Su, H., Mo, K., & Guibas, L. J. (2017). Pointnet: Deep learning on point sets for 3d classification and segmentation. In Proceedings of the IEEE conference on computer vision and pattern recognition (pp. 652-660)](https://openaccess.thecvf.com/content_cvpr_2017/html/Qi_PointNet_Deep_Learning_CVPR_2017_paper.html)