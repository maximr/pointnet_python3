#pointnet
Deep neural networks that directly consume point cloud for 3D classification and segementation, implemented in TensorFlow.

![prediction example](https://github.com/charlesq34/pointnet/blob/master/doc/teaser.png)

### Fix for Python3

This is the pointnet TF library with some monkey patches for python3 & mac os support...

### Introduction
This work is based on our [arXiv tech report](https://arxiv.org/abs/1612.00593), where we proposed a novel deep net architecture for point clouds (as unordered point sets). You can also check our [project webpage](http://stanford.edu/~rqi/pointnet) for a deeper introduction.

Point cloud is an important type of geometric data structure. Due to its irregular format, most researchers transform such data to regular 3D voxel grids or collections of images. This, however, renders data unnecessarily voluminous and causes issues. In this paper, we design a novel type of neural network that directly consumes point clouds, which well respects the permutation invariance of points in the input.  Our network, named PointNet, provides a unified architecture for applications ranging from object classification, part segmentation, to scene semantic parsing. Though simple, PointNet is highly efficient and effective.

In this repository, we release code and data for training a PointNet classification network on point clouds sampled from 3D shapes.

### Citation
If you find our work useful in your research, please consider citing:

	@article{qi2016pointnet,
	  title={PointNet: Deep Learning on Point Sets for 3D Classification and Segmentation},
	  author={Qi, Charles R and Su, Hao and Mo, Kaichun and Guibas, Leonidas J},
	  journal={arXiv preprint arXiv:1612.00593},
	  year={2016}
	}
   
### Installation

Install <a href="https://www.tensorflow.org/get_started/os_setup" target="_blank">TensorFlow</a>. You may also need to install h5py. The code has been tested with TensorFlow 0.12.1, CUDA 8.0 and cuDNN 5.1 on Ubuntu 14.04.

### Usage
To train a model to classify point clouds sampled from 3D shapes:

    python train.py

Log files and network parameters will be saved to `log` folder in default. Point clouds of <a href="http://modelnet.cs.princeton.edu/" target="_blank">ModelNet40</a> models in HDF5 files will be automatically downloaded (416MB) to the data folder. Each point cloud contains 2048 points uniformly sampled from a shape surface. Each cloud is zero-mean and normalized into an unit sphere. There are also text files in `data/modelnet40_ply_hdf5_2048` specifying the ids of shapes in h5 files.

To see HELP for the training script:

    python train.py -h

We can use TensorBoard to view the network architecture and monitor the training progress.

    tensorboard --logdir log

After the above training, we can evaluate the model and output some visualizations of the error cases.

    python evaluate.py --visu True

Point clouds that are wrongly classified will be saved to `dump` folder in default. We visualize the point cloud by rendering it into three-view images.

If you'd like to prepare your own data, you can refer to some helper functions in `utils/data_prep_util.py` for saving and loading HDF5 files.

### License
Our code is released under MIT License (see LICENSE file for details).

### TODO

Add test script for evaluation on OOS shape or point cloud data.

Add example code for training segmentation networks.
