<hr>

## Problem with PointNet
PointNet does not capture local structures induced by the metric space in which points are present, limiting its ability to recognize fine-grained patterns and generalizability to complex scenes.

## PointNet++
A hierarchical neural network that applies PointNet recursively.

#### How it works
PointNet++ divides a set of points into overlapping local regions based on the underlying space's distance measure. Similar to CNNs, it extracts local features from tiny neighborhoods, capturing fine geometric structures, and then groups these local features into bigger units and processes them to produce higher-level features. This technique is repeated until the entire point set's features are obtained.

It Solves two problems:

- How to generate the partitioning of the point set
- How to abstract sets of points or local features through a local feature learner

PointNet uses only a single max-pooling operation to aggregate the whole point set, while the PointNet++ builds a hierarchical grouping of points and progressively abstract larger local regions along the hierarchy.

The hierarchical structure of PointNet++ is composed of abstraction levels and at each one, a set of points is processed and abstracted to produce a new set with fewer elements.

The abstraction layer is made of three layers:

- Sampling layer: Selects a set of points from input points, which defines the centroids of local regions.
- Grouping layer: Constructs local region sets by finding “neighboring” points around the centroids.
- PointNet layer: Uses a mini-PointNet to encode local region patterns into feature vectors.

<div style="text-align: center;">
    <img src="../images/network_image.jpg">
</div>

## Resources
- [3D Point Cloud Semantic Segmentation Using Deep Learning Techniques](https://medium.com/analytics-vidhya/3d-point-cloud-semantic-segmentation-using-deep-learning-techniques-6c4504a97ce6)
- Main Paper: [Qi, C. R., Yi, L., Su, H., & Guibas, L. J. (2017). Pointnet++: Deep hierarchical feature learning on point sets in a metric space. arXiv preprint arXiv:1706.02413.](https://arxiv.org/abs/1706.02413)