# Safety Vests Detector<br/><br/>

## Were implemented 2 solutions to detect the safety vests:



## 1)Person detection + color detection (full video in repo)
![person detection color detection](./color_detection.gif)
<br/><br/><br/><br/>
## 2)Retinanet trained model  (full video in repo)
![retinanet trained model](./retinanet.gif)

## For the first solution you don't need to train the model. Just clone the repo and have installed tensorflow, keras and dependecies.

## To detect safety vests using retinanet trained model, we need to train it:

# Setting up training
## P.S you can skip the training, by downloading my weights https://drive.google.com/file/d/1GnFp8QMWBuYr8r1v94ibizKr4pS_gyEJ/view?usp=sharing

### Clone keras-retinanet repo in ~/safety_vests_detection (folder of current repo):<br/>
git clone https://github.com/fizyr/keras-retinanet.git



```console
change list of classes in /keras-retinanet/keras_retinanet/preprocessing/pascal_voc.py
```

```python

voc_classes = {
    'safety_vest' : 0
}
```

```console
cd ./keras-retinanet/
python3 setup.py build_ext --inplace
```
<br/><br/>
# Train the model

### download PlumsVOC folder from https://drive.google.com/file/d/11BetQCcj8z0KIhNSeOrB_gKkkq47A4ki/view?usp=sharing and place it in this repo

## Make directory to save the snaphots: <br/>
```console
mkdir -p TrainingOutput/snapshots

```

## Run the training

```console
python3 keras_retinanet/bin/train.py --tensorboard-dir ./TrainingOutput --snapshot-path ./TrainingOutput/snapshots --random-transform --steps 100 pascal ./PlumsVOC
```

### To monitor the progress of training open tensorboard:

Run tensorboard in a new terminal using
```console
tensorboard --logdir ./TrainingOutput
```
<br/>
then open http://localhost:6006/ in a browser tab

# Predict
Convert the latest(best) model to an inference mode: <br/><br/>
```console
python3 keras_retinanet/bin/convert_model.py ./TrainingOutput/snapshots/WEIGHTSNAME.h5 ./RetinanetModels/PlumsInference.h5
```

## Now you can run scripts for video processing

video_processing(retinanet).ipynb
### or
video_processing(rcnn+opencv).ipynb

# Accuracy improving
### The accuracy of model can be improved with implementation of object tracking and increacing the amount of training data. Also tuning of confidence threshold for detection can yield some benefits.
