# Masterproject: 3D pose estimation from a single 2D image

This is the accompanying code and data for my masterproject.

## Abstract

Building a 3D scene from a 2D image finds an application in many different fields, such as robotics and computer vision. 
My Project focuses on a subtopic of that, namely the challenge of getting an object's 3D Pose Estimation from a single 2D image. 
Because of limited amounts of training data, many methods rely on synthetic, rendered images.


The method proposed here works solely on real images, exploiting similarities between different shape classes. It is based on [[1]](#1) and predicts the closest shape out of a model database and estimates the corresponding 3D rotation from a single image.
This is done in two stages, where in the first stage, a general embedding is learnt from the volumetric representations of the available shapes, and in the second stage an image is mapped to the embedding. 

This outperforms any previously recorded results on the 'in the wild' dataset PASCAL3D+ by a wide margin and even performs notably better than [[1]](#1) itself.

The proposed method also outputs an uncertainty value and therefore makes it easier to 
spot rotational ambiguities of the pose.
In future, this could for example provide a robot with more accurate instructions on how to interact with the environment, by better assessing its possible actions.

My implementation takes only several hours to train on a single GPU, which makes it ideal for quickly testing new hypotheses.

---
<a id="1">[1]</a> 
Kyaw Zaw Lin, Weipeng Xu, Qianru Sun, Christian Theobalt, and Tat-Seng Chua.
Learning a Disentangled Embedding for Monocular 3D Shape Retrieval and Pose Estimation. arXiv e-prints, page arXiv:1812.09899, December 2018.


## Instructions to run
1. Download the repository
2. Install all libraries and dependencies in a conda virtual environment
     1. download and install [conda](<https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html>)
     1. install libraries by runnning `conda env create -f environment.yml` ([docs](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-from-an-environment-yml-file))
within the main folder of this repository.
     1. activate the new virtual environment: `conda activate masterproject`
3. Download and Pre-process the images and annotations as described in **Data**
2. Find a description of possible command line arguments by running
```
python3 inplementation.py -h
```

The only required argument is an experiment name. It can be specified with `-n`.
So, for example, `python3 implementation.py -n 'my_experiment'` will run the code and save the results with the name 'my_experiment'.


## Data
The dataset PASCAL3D+ can be found [here](https://cvgl.stanford.edu/projects/pascal3d.html). I am using version 1.1.

There are two pre-processing parts. One is a notebook for the images and annotations (_pre_processing-images_and_annotations.ipynb_)
and the other is a python program for the 3D models (_pre_processing_pointclouds.py_).

The pointclouds are already part of this repository, but the images and annotations have to be created:
1. Make sure that the PATHS at the top of _pre_processing-images_and_annotations.ipynb_ are correct.
2. Run the notebook
3. confirm that everything worked, by checking the Data/numpy_data/ folder. It should contain one Test and one Train folder, each with subfolders for every class that contain images, bboxes, shape_idxs, valid_im_ids, occluded, truncated and true_rots.


The pointcloud pre-processing was done with MeshLab. 
After it is installed ([MeshLab Installation](http://www.meshlab.net/#download)), change the paths in _pre_processing_pointclouds.py_ accordingly.


## Results
An overview over the results and corresponding parameter values can be found in _trained_nets/results/_.
_Display_results.ipynb_ displays them.

