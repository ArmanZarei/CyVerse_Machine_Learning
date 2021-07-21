<hr>

## GAN
GANs are a framework for teaching a DL model to capture the training data’s distribution so we can generate new data from that same distribution. GANs were invented by Ian Goodfellow in 2014. 

They are made of two distinct models, a **generator** and a **discriminator**

- Job of generator: generating 'fake' images that look like the training images.
- Job of discriminator: look at an image and output whether or not it is a real training image or a fake image from the generator

During training, the generator is constantly trying to outsmart the discriminator by generating better and better fakes, while the discriminator is working to become a better detective and correctly classify the real and fake images.

The equilibrium of this game is when the generator is generating perfect fakes that look as if they came directly from the training data, and the discriminator is left to always guess at 50% confidence that the generator output is real or fake.

#### Some notations
- $D(x)$ is the discriminator network which outputs the (scalar) probability that $x$ came from training data rather than the generator
    - Here, since we are dealing with images, $x$ is an image of size $3 \times 64 \times 64$
    - $D(x)$ should be **high** when $x$ comes from **training data** and **low** when $x$ comes from the **generator**
- $G(z)$ represents the generator function which maps the latent vector $z$ to data-space.
    - $z$ is a latent space vector sampled from a standard normal distribution
    - The goal of $G$ is to estimate the distribution that the training data comes from ($p_{data}$) so it can generate fake samples from that estimated distribution ($p_g$)
- So, $D(G(z))$ is the probability (scalar) that the output of the generator $G$ is a real image.

#### Loss function
$D$ and $G$ play a minimax game in which

- $D$ tries to maximize the probability it correctly classifies reals and fakes $\rightarrow log(D(x))$
- $G$ tries to minimize the probability that $D$ will predict its outputs are fake $\rightarrow log(1-D(G(z)))$

From the paper, the GAN loss function is:

$min_G \; max_D \; V(D, G) = \mathbb{E}_{x \sim p_{data}(x)}[log(D(x))] + \mathbb{E}_{z \sim p_z(z)}[log(1-D(G(z)))]$

In theory, the solution to this minimax game is where $p_g = p_{data}$, and the discriminator guesses randomly if the inputs are real or fake. However, the convergence theory of GANs is still being actively researched and in reality models do not always train to this point.
## DCGAN
Deep Convolutional Generative Adversarial Networks (DCGAN) is a direct extension of the GAN, except that it explicitly uses convolutional and convolutional-transpose layers in the discriminator and generator, respectively.

More details of implementation can be found in the link below

## Source Code
[Link](https://github.com/ArmanZarei/DCGAN_PyTorch/blob/main/DCGAN.ipynb)

## Resources
- [DCGAN Tutorial - PyTorch](https://pytorch.org/tutorials/beginner/dcgan_faces_tutorial.html)