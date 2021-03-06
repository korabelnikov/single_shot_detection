# Single Shot Detection
Build flexible object detection pipelines with declarative configuration
### Content
You are being provided with the following set of features:
- Supporting latest PyTorch release
- Train SSD or RetinaNet
- Available backbones: torchvision + MobileNet, MobileNetV2
- Data augmentations
- [AdamW and SGDW](https://www.fast.ai/2018/07/02/adam-weight-decay/) optimizers, some custom learning rate schedulers
- Weight pruning for efficient inference
- Export to [ONNX](https://github.com/onnx/onnx) or [OpenVINO](https://github.com/opencv/dldt)
- Tensorboard integration
- Training callbacks

### Quick start
Download [PASCAL VOC](http://host.robots.ox.ac.uk/pascal/VOC/) or [COCO](http://cocodataset.org/) dataset and start training using one of the provided sample configs:
```
python3 main.py --config samples/ssd_mb2_voc.py
```
<sup><sup>(don't forget to adjust the path first!)</sup></sup>
#### Command line arguments:
- `config` - a path to a config file
- `save_dir` - a folder where checkpoints are going to be saved
- `checkpoint_dir` - set this to restore training from a previously created checkpoint. All subsequent checkpoints will saved here instead of `save_dir` unless `new_checkpoint` arguments is specified
- `phases` - one or multiple runtime phases:
    - `train` - run train loop
    - `eval` - run eval pass; if is set along with `train` runs each `eval_every`'th epoch
    - `test` - run on a video, drawing annotations
    - `export` - export to ONNX
    - `export-mo` - export to OpenVINO model format
    - `embed` - *(for debug purposes)* drop to IPython shell after initialization
- `video` - a video or a folder (which will be searched recursively) for `test` phase
- `tensorboard` - save tensorboard log to the checkpoint folder
### Requirements
- `python 3.6`
- `opencv` with python bindings
- `requirements.txt`
### Structure
Some places that may be useful to look into:
- `bf` - provides common reusable parts for building a deep learning pipeline
    - `bf.base` - custom backbone network implementation (e.g. MobileNetV2)
    - `bf.datasets` - dataset handling
    - `bf.preprocessing` - data augmentations and preprocessing
    - `bf.training` - callbacks; custom optimizers and learning
    rate schedulers; weight prunner
    - ...
- `detection` - parts of code which are used to build object detection pipelines on top of `bf`
- `samples` - contains sample configuration files for popular network architectures
- `main.py` - the entry point
### Inspired by
- Tensorflow Object Detection API (https://github.com/tensorflow/models/tree/master/research/object_detection)
- Gluon CV (https://github.com/dmlc/gluon-cv)
