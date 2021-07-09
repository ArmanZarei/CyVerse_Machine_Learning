<hr>

## Limitations of existing methods:
<ol>
    <li>
    Most approaches are limited to <strong>extremely</strong> 3D point clouds. methods like:
        <ul>
            <li>PointNet</li>
            <li>PointNet++</li>
            <li>PointCNN</li>
            <li>PCCN</li>
            <li>ShellNet</li>
        </ul>
    </li>
    <li>
    Few methods can directly process large-scale point clouds, but they either rely on <strong>time-consuming preprocessing</strong> or <strong>computationally expensive voxelization steps</strong>.
    methods like:
        <ul>
            <li>SPG</li>
            <li>FCPN</li>
            <li>TagentConv</li>
            <li>PCT</li>
        </ul>
    </li>
</ol>

## Goal
Develope a method that is

- **Process large-scale point clouds directly**
    - Without <span style="color: #c0392b">block partition</span> and block merging
    - Take the <span style="color: #c0392b">whole geometry</span> into consideration
- **Computationally efficient & Memory efficient**
    - Without time-consuming <span style="color: #c0392b">preprocessing</span> or <span style="color: #c0392b">voxelization</span> steps
    - inference a large-scale point cloud in a single pass
- **Effective & Accurate**
    - Complex geometrix structures
    - Capture and preserve the <span style="color: #c0392b">prominent</span> features

## Key Problems
- Efficient **point sampling** to reduce memomry footprint and computational cost
- Effective **local feature aggregatiion** to capture the geometrical patterns

<br>
<img src="../images/heuristic_sampling_1.PNG" style="width: 75%;">
<img src="../images/heuristic_sampling_2.PNG">

So we have the problem of "discarding useful features" in Random Point Sampling. To solve this problem, Local Feature Aggregation is proposed.

## Local Feature Aggregation
<div style="text-align: center;">
    <img src="../images/network.png">
</div>

### Local Spatial Encoding
<ol> 
    <li>Find the neighboring points for each point by using KNN</li>
    <li>Explicitly encode the relative point position of all neighboring points so that the corresponding point features are always aware of their relative spatial locations. this tends to aid the network to captures the geometric patterns.</li>
    <li>Encoded relative point position features are concatenated with its corresponding point features.</li>
</ol>

### Attentive Pooling
Goal: Aggregate the neighboring feature set
Instead of using max or mean pooling to hard integrade the neighboring features (majority of information has been lost), we turn to the powerful attention mechanism to automatically learn important local features from the neighboring feature set.
<ol>
    <li><strong>Computing attention scores</strong>: with a shared function \(g\) to learn a unique attention score for each feature</li>
    <li><strong>Weighted Summation</strong>: \(\widetilde{f_i}\) which is the aggregated features</li>
</ol>

### Dilated Redidual Block
Since the large point clouds are going to be substantially down-sampled, it is desirable to significantly increase the receptive field of each point (so that geometric details are more likely to reserved even if some points are dropped).

So multiple spatial encoding and attentive pooling units are stacked together with a skip connection as a dilated residual block.  

<div style="text-align: center;">
    <img src="../images/increase_of_receptive_field.png">
</div>

### RandLA-Net Architechture

<div style="text-align: center;">
    <img src="../images/RandLANet_architecture.PNG">
</div>