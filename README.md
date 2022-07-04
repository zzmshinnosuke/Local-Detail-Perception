# 20220704
在3090上不行，会卡在一个地方很长时间，开始运行后，loss会变成NAN。在2080ti和titan上可以正常运行，cuda10.1和environment中的tensorflow1.15版本匹配。3090只能支持cuda11.1以上的版本，以后不在上面瞎尝试了，没有一次成功的。最后titan上这两天没人用，完全转移到titan上跑。   
安装过程中可以使用`conda env create -f environment.yml`进行安装，但是会提示pydensecrf和cairocffi找不到的错误，可以从environment中删除了这两项，其中cairocffi好像没啥用，没按也没影响，pydensecrf可以按以下命令安装。  
```
pip install cython  
pip install git+https://github.com/lucasb-eyer/pydensecrf.git  
```
里边还有一些参数类型错误的问题，不知道作者是怎么跑起来的。

# Exploring Local Detail Perception for Scene Sketch Semantic Segmentation

Code release for ["Exploring Local Detail Perception for Scene Sketch Semantic Segmentation"](https://doi.org/10.1109/TIP.2022.3142511) (IEEE TIP)

## Requirements

- Create a conda environment from the `environment.yml` file:
```bash
conda env create -f environment.yml
```

- Activate the environment: 

```bash
conda activate LDP
```

## Preparations

- Get the code:

```bash
git clone https://github.com/drcege/Local-Detail-Perception && cd Local-Detail-Perception
```

- Download datasets from [releases](https://github.com/drcege/Local-Detail-Perception/releases) and place them under the `datasets` directory following its instructions.

- Generate ImageNet pre-trained "ResNet-101" model in TensorFlow version for initial training and place it under the `resnet_pretrained_model` directory. This can be obtained following the instructions in [chenxi116/TF-resnet](https://github.com/chenxi116/TF-resnet#example-usage). For convenience, the converted model can be downloaded from [here](https://drive.google.com/drive/folders/11sI3IARgAKTf4rut1isQgTOdGKFeyZ1c?usp=sharing).

## Training

```bash
python3 segment_main.py --mode=train --run_name=LDP 
```

## Evaluation

```
python3 segment_main.py --mode=test --run_name=LDP
```

## Credits

- The ResNet-101 model pre-trained on ImageNet in TensorFlow is created by [chenxi116](https://github.com/chenxi116/TF-resnet)
- The code for the DeepLab model is authored by [Tensorflow authors](https://github.com/tensorflow/models/blob/master/research/resnet/resnet_model.py) and [chenxi116](https://github.com/chenxi116/TF-deeplab)
- The repository is developed based on [SketchyScene](https://github.com/SketchyScene/SketchyScene)

