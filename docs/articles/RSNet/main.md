## Problem with other semantic segmentation networks
Not modelling required dependencies between cloud points.

## Key component in RSNet
### lightweight local dependency module

The local dependency module is highly efficient and has the time complexity of the slice pooling/unpooling layer as $O(n)$ w.r.t the number of input points and $O(1)$ w.r.t the local context resolutions.

## RSNet Components

- ### Input feature extraction block
input points $\rightarrow$ features
- ### Local dependency module
Combination of
    - Slice pooling layer
    - Bidirectional Recurrent Neural Network (RNN) layers
    - Slice unpooling layer

**local context problem** is solved by first **projecting unordered points into ordered features** and then **applying traditional end-to-end learning algorithms**

The projection is achieved by a novel **slice pooling layer**

<ol>
    <li>
        <strong>Slice pooling layer</strong>
        <p>input: features of unordered points \(\rightarrow\) output: ordered sequence of aggregated features</p>
    </li>
    <li>
        <strong>RNN layers</strong>
        <p>Next, RNNs are applied to <strong>model dependencies</strong> in this sequence.</p>
    </li>
    <li>
        <strong>Slice unpooling layer</strong>
        <p>Finally, a slice unpooling layer <strong>assigns features in the sequence back to points</strong>.</p>
    </li>
</ol>

- ### Output feature extraction block
processed features $\rightarrow$ final predictions for each point

**Note:** Both input and output blocks use a sequence of multiple $1 \times 1$ convolutional layers to produce independent feature representations for each point.

<div style='text-align: center;'>
    <img src='../images/architechture.PNG'>
</div>