# HANet

![The framework of HANet](./docs/assets/HANet.png)

## Contributions

- We propose a novel approach HANet that utilizes the keypoints’ kinematic features, following the laws of physics. Our method addresses temporal issues with these proposed features, effectively mitigates the jitter, and becomes robust to occlusion.

- We propose a hierarchical transformer encoder that incorporates multi-scale spatio-temporal attention. We use multi-scale feature maps, i.e., leverage all layers’ attention maps, and improve performance on benchmarks that provide sparse supervision.

- We propose online mutual learning that enables joint optimization between refined input poses and final poses, which chooses an online learning target by their training losses.

- We conduct extensive experiments on large datasets and demonstrate that our framework improves performance on tasks: 2D pose estimation, 3D pose estimation, body mesh recovery, and sparsely-annotated multi-human 2D pose estimation.

## Getting Started

### Environment Requirement

HANet has been implemented and tested on Pytorch 1.10.1 with python = 3.6. It supports both GPU and CPU inference.

Clone the repo:

```bash
git clone https://github.com/wacv1686/HANet.git
```

We recommend you install the requirements using `conda`:

```bash
# conda
conda create env --name HANet python=3.6
conda activate HANet
pip install -r requirements.txt
```

### Prepare Data

We prepare all the datasets as soon as possible. Sub-JHMDB data used in our experiment can be downloaded here.

[Google Drive](https://drive.google.com/drive/folders/1uLpuRcRbbVqmyndCnuuaW7qRACJaqMX1?usp=sharing)

Valid data includes:

| Dataset                                  | Pose Estimator                                                               | 3D Pose | 2D Pose | SMPL |
| ---------------------------------------- | ---------------------------------------------------------------------------- | ------- | ------- | ---- |
| [Sub-JHMDB](http://jhmdb.is.tue.mpg.de/) | [SimpleBaseline](https://github.com/microsoft/human-pose-estimation.pytorch) |         | ✔       |      |

### Training

Note that the training and testing datasets should be downloaded and prepared before training.

Run the commands below to start training:

```shell script
python train.py --cfg [config file] --dataset_name [dataset name] --estimator [backbone estimator you use] --body_representation [smpl/3D/2D]
```

For example, you can train on **2D position representation** of the **jhmdb dataset** using the **backbone estimator simplebaseline** (sampling ratio=10%) by:

```shell script
python train.py --cfg configs/config_jhmdb_simplebaseline_2D.yaml --dataset_name jhmdb --estimator simplebaseline --body_representation 2D
```

### Evaluation

**Results on 2D Pose:**

| Dataset   | Estimator      | PCK 0.05 (Input/Output):arrow_up: | PCK 0.1 (Input/Output):arrow_up: | PCK 0.2 (Input/Output):arrow_up: | Checkpoint                                                                                           |
| --------- | -------------- | --------------------------------- | -------------------------------- | -------------------------------- | ---------------------------------------------------------------------------------------------------- |
| Sub-JHMDB | simplebaseline | 57.3%/88.7%                       | 81.6%/97.5%                      | 93.9%/99.5%                      | [Google Drive](https://drive.google.com/drive/folders/11A5NFkViDgQNyCGGwsmhAbUkwmV36M-E?usp=sharing) |

## Visualization

We prepare all visualization codes as soon as possible.

### 2D Pose

Visualize comparison on Sub-JHMDB

![visualize of Sub-JHMDB 2D SimpleBaseline](./docs/assets/jhmdb.gif)

### 3D Pose

Visualize comparison on AIST++

![visualize of AIST++ 3D SPIN](./docs/assets/aist_3D.gif)

### 3D Body Mesh Recovery

Visualize comparison on 3DPW PARE

![visualize of AIST++ SMPL SPIN](./docs/assets/pw3d_smpl.gif)

Visualize comparison on AIST++ SPIN

![visualize of AIST++ SMPL SPIN](./docs/assets/aist_smpl.gif)
