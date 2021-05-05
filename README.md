# Pix2Vox-B657-Experiments
Implementation of "Pix2Vox: Context-aware 3D Reconstruction from Single and Multi-view Images" (Xie et al., ICCV 2019)

See the original Readme here:
  
https://github.com/codyharris91/Pix2Vox-B657-Experiments/blob/master/original_README.md

ShapeNet Data Download:
http://cvgl.stanford.edu/data2/ShapeNetRendering.tgz
http://cvgl.stanford.edu/data2/ShapeNetVox32.tgz

Pre-Trained Weights from Our Experiments:
https://drive.google.com/drive/folders/13dFtxluwZVHGzdwDFGc6fAkexoH60vlk?usp=sharing

## Preliminary steps to implement

1. Clone this repo  
2. Download and extract the ShapeNet Data  
3. In the datasets folder, insert both the ShapeNetRendering and ShapenetVox32 folders  
4. If you would like you can download our pre-trained weights from the link above

## Training

To train you must decide the images you would like to train on. This is done by changing the file /datasets/ShapeNet.json

The current ShapeNet.json will train on all the data that Pix2Vox trained on. We have prepared a folder "training_json" that includes the files that we used in our experiments.
Pick an experiment, rename the json to ShapeNet.json and replace it in the /datasets folder.

If you would like to change the number of views used, edit the config file in the root directory. Change the value of:
__C.CONST.N_VIEWS_RENDERING

To a number you would like. You might need to also change __C.CONST.BATCH_SIZE depending on your hardware.

Navigate to the directory of this project and run the following command

```
python3 runner.py --weights=/folder/with/weights/weights.pth
```

This will output the best weights every 10 epochs (can be changed in the config file) into the /output/checkpoints folder.

## Testing

To choose the images tested on, follow the instructions from the Training section as the testing images are selected using the ShapeNet.json file as well.

The following command runs a test of the pretrained weights used to output some summary statistics of the results

```
python3 runner.py --test --weights=/folder/with/weights/weights.pth
```

## View the results of a single image run through the network

Use the following command:

```
python3 runner-single.py --test --in=/image.png --out=/output/folder/ --weights=/folder/with/weights/weights.pth
```

This will output an image to the specified output folder that is the estimated model for the image specified.
