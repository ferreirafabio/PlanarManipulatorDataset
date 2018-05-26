# Planar (Robot) Manipulator Dataset
The dataset consists of 90 000 color videos that show a planar robot manipulator executing articulated manipulation tasks. More precisely, the manipulator grasps a circular object of random color and size and places it on top of a square object/platform of again random color and size.
The initial conﬁgurations (location, size and color) of the objects were randomly sampled during generation. Different from other datasets such as the moving MNIST dataset, the samples comprise a goal-oriented task as described, making it more suitable for testing prediction capabilities of an ML model.For instance, one can use it as a toy dataset to investigate the capacity and output behavior of a deep neural network before testing it on real-world data. We have done this for a deep auto-encoder network:

![Example 1](/examples/orig1.gif)
![Example 2](/examples/orig2.gif)
![Example 1](/examples/orig3.gif)  
![Example 1 generated](/examples/gen1.gif)
![Example 2 generated](/examples/gen2.gif)
![Example 3 generated](/examples/gen3.gif)

To accesss a similar dataset see ![Simulated Flying Shapes Dataset](https://github.com/ferreirafabio/FlyingShapesDataset)

# Download
Automatically download the data by using the included scripts:
- ```python download_videos.py``` (.tar files ~1.3GB, uncompressed ~23GB) or 
- ```python download_tfrecords.py``` for the tfrecords respectively (~89 GB)

or manually download them by invoking the download links in the files
- ```planarmanipulator_videos.txt```
- ```planarmanipulator_tfrecords.txt```

# Citing
If you use the dataset in your research, you should cite it as follows:

```
@misc{npde2018,
    author = {Fabio Ferreira, Jonas Rothfuss, Eren E. Aksoy, You Zhou},
    title = {Introducing the Simulated Flying Shapes and Simulated Planar Manipulator Datasets},
    year = {2018},
    publisher = {GitHub},
    journal = {GitHub repository},
    howpublished = {\url{https://github.com/ferreirafabio/PlanarManipulatorDataset}},
}
```
## TODO
# Specifications
We provide both the videos as .avi files as well as TensorFlow tfrecord files. The samples in the tfrecord files contain 10 frames of the original video which were taken equally distributed over the entire playtime. Here are some more details:
## Dataset as avi
- video resolution: 128x128
- fps: 30
- color depth: 24bpp (3 channels, grayscale)
- video codec: ffmjpeg
- compression format: mjpeg, color encoding: yuvj420p
- the samples follow the naming: 
  ```
  id_shape_startLocation_endLocation_motionDirection_euclideanDistance
  ```
  where:
    - ```id``` is a unique identifier
    - ```startLocation``` starting position of the object, e.g. righttop
    - ```endLocation``` destination position of the object, e.g. leftbottom
    - ```motionDirection``` e.g. left
    - ```euclideanDistance``` Euclidean distance between the two objects, e.g. 7.765617 

## Dataset as tfrecord
The tfrecord files store both the video itself and meta information from the file name (start location, eucl. distance etc.).
- the video data is stored in a ```feature``` dict (which is serialized as ```tf.train.Example```) which stores the following keys 
    - feature[path] #('blob' + '/' + str(imageCount)
    - feature['height']
    - feature['width']
    - feature['depth']
    - feature['id']
- additional information is stored in a ```meta_dict``` (which is also serialized within the feature dict via the key 'metadata')
    - meta_dict['shape']
    - meta_dict['start_location']
    - meta_dict['end_location']
    - meta_dict['motion_location']
    - meta_dict['eucl_distance']
