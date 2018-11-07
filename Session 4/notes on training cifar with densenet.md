Accuracy 88 %

Parameter-4 million

Augmentation-

```
datagen = ImageDataGenerator(zoom_range=0.2, 
                             horizontal_flip=True)
```

https://github.com/shankarj67/Mlblr/blob/master/DenseNet%20on%20CIFAR-10%20Datasets.ipynb



```
#data augmentation
datagen ``=` `ImageDataGenerator(
    ``rotation_range``=``15``,
    ``width_shift_range``=``0.1``,
    ``height_shift_range``=``0.1``,
    ``horizontal_flip``=``True``,
    ``)
datagen.fit(x_train)
```

https://appliedmachinelearning.blog/2018/03/24/achieving-90-accuracy-in-object-recognition-task-on-cifar-10-dataset-with-keras-convolutional-neural-networks/

Parameter 118k

imgaug

Accuracy 80%

https://github.com/leoninekev/applied-ML-MLBLR-/blob/master/assignment_4/Image%20augmention%20for%20CIFAR%2010%20classification%20densenet_4B.ipynb





68k 

Accuracy 78%

https://github.com/leoninekev/applied-ML-MLBLR-/blob/master/assignment_4/Implementing%20Densenet%20for%20classifying%20CIFAR%2010%20data%20on%20Keras_4B%20.ipynb





Pydrive 

https://github.com/rraghu214/MLBLR/blob/master/RAGHU_BATCH_5_ASSIGNMENT4B.ipynb



Interesting thoughts/pointers/resources :

1.Densely Connected Convolutional Networks - [https://arxiv.org/pdf/1608.06993.pdf (Links to an external site.)Links to an external site.](https://arxiv.org/pdf/1608.06993.pdf)

2.Enhanced Deep Residual Networks for Single Image Super-Resolution - [https://arxiv.org/pdf/1707.02921.pdf (Links to an external site.)Links to an external site.](https://arxiv.org/pdf/1707.02921.pdf) , this has details on ways of selecting depth and width parameters in the CNN under "3.2. Single-scale model" section.

3.The given code doesn't seem to be working for variable image sizes. Looks like there is blocking code.

It appears, currently training the model to a decent accuracy is taking huge time (order of hours). If anyone has suggestions on how to train the model faster ,it would be great. Please note increasing the batch size is not helping as its causing OOM from GPU :-(.





Blogs

https://medium.com/intuitionmachine/notes-on-the-implementation-densenet-in-tensorflow-beeda9dd1504

https://github.com/ikhlestov/vision_networks/blob/master/models/dense_net.py

https://github.com/liuzhuang13/DenseNet

https://github.com/liuzhuang13/DenseNet#results-on-cifar

https://github.com/flyyufelix/DenseNet-Keras/blob/master/test_inference.py

https://github.com/flyyufelix/cnn_finetune/blob/master/densenet121.py

Cyclical Learning Rate

https://github.com/bckenstler/CLR/blob/master/clr_callback_tests.ipynb



Approach

Train on lower resolution image.Het 92% accuracy 

DO model checkpoint-get codes from discussion





COde snippet for imgaug with cifar10

https://github.com/YixuanLi/densenet-tensorflow/blob/master/cifar10-densenet.py





Reduce kernel size using 1x1 in dense block

**Architecture**

# Dense Block
def add_denseblock(input, l, num_filter = 16, dropout_rate = 0.2):
​    global compression
​    temp = input
​    for _ in range(l):
​        BatchNorm = BatchNormalization()(temp)
​        relu = Activation('relu')(BatchNorm)
​        #Conv2D_1_1 = Conv2D(int(num_filter*compression),(1,1), use_bias= False, padding='same')(relu)
​        #BatchNorm = BatchNormalization()(Conv2D_1_1)
​        #relu = Activation('relu')(BatchNorm)
​        Conv2D_3_3 = Conv2D(int(num_filter*compression), (3,3), use_bias=False ,padding='same')(relu)
​        if dropout_rate>0:
​          Conv2D_3_3 = Dropout(dropout_rate)(Conv2D_3_3)
​        concat = Concatenate(axis=-1)([temp,Conv2D_3_3])
​        
​        temp = concat
​        
​    return temp


Is it test time augmentation

https://github.com/jacobswan1/keras-for-second-order-based-SGD/blob/master/examples/cifar10_cnn.py



# Image Augmentation for Deep Learning using Keras and Histogram Equalization

https://towardsdatascience.com/image-augmentation-for-deep-learning-using-keras-and-histogram-equalization-9329f6ae5085



A beeter way to get a summary

https://blog.plon.io/tutorials/cifar-10-classification-using-keras-tutorial/

sequential_model_to_ascii_printout(cnn_n)



Correct normalization value

Correct normalization values for CIFAR-10: (0.4914, 0.4822, 0.4465), (0.247, 0.243, 0.261)

https://github.com/Armour/pytorch-nn-practice/blob/master/utils/meanstd.py



Good blog of cifar10 on tensorflow

https://towardsdatascience.com/cifar-10-image-classification-in-tensorflow-5b501f7dc77c

https://github.com/deep-diver/CIFAR10-img-classification-tensorflow/blob/master/CIFAR10_image_classification.ipynb



Keypoints for cifar10

https://medium.com/intuitionmachine/notes-on-the-implementation-densenet-in-tensorflow-beeda9dd1504

https://github.com/flyyufelix/DenseNet-Keras/blob/master/densenet121.py



Saving models

You can save with a file name like 'model.h5' but the problem is that it can store model with val_acc as per its last epoch, which can be lesser than the highest val_acc model has reached in any previous epoch.

On the other hand by using file name as 'model_name-{epoch:02d}-{val_acc:.2f}.hdf5', model stores weights for the best val_acc attained along.



Architecture to explore

https://github.com/flyyufelix/cnn_finetune/blob/master/densenet121.py



Improving training accuracy

https://towardsdatascience.com/different-ways-of-improving-training-accuracy-c526db15a5b2