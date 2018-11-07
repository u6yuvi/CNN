Session 4 Notes

Add

Subtract

Multiply

Divide

Concatenate-It is used heavily in style transfer.



Accuracy

Top k categorical accuracy

Actual category is compared with top 5 predicted category.

True if top 5 predicted category consist of actual category or else False



 Recognition vs Detection



## Detection Approaches

Simplify Object Detection problem by:

1. ignoring lower prediction values
2. predicting bounding boxes instead of exact object mask
3. mixing different receptive field layers
4. ....but this is easier said than done.



Different approach to Detection problem

1.Yolo 

2.SSD





How to Compute a good candidate  Anchor Boxes	

***Note***  In yolo the detection works on 13x13 receptive field(image_size)

we have an image of size 220x240 and accordingly we will have our bounding box with dimension smaller or equal to this image size

1.standardize the values by its resolution to first make the image size 1x1  get the values of bounding box ranging between 0 and 1.

While mean of maximum IOU between the bounding box and individual anchors is not satisfactory:

​	1.Run k-means clustering  to cluster bounding box features(height and width)

​	2.Use centroid(height,width of anchor boxes) of a cluster to choose potential anchor boxes 



In yolov2 ,5 anchor boxes was chosen with mean IOU was above 65%

***Note:***Each anchor box is specialized for particular aspect ratio and size







How y_train is prepared

1. Receptive field is divided into 13x13 cells

3.Identify the grid cell having the image (grid cell which has the centre of bounding box).

4.Locate the centre of the grid cell (x_c,y_c)

5.Calculate height and width of the bounding box from centroid .

6.



After obtaining few good candidate we choose one template for each image by comparing IOU between Anchor box and bounding box.

Labels in our training sample

1.Grid cell

2.Template number(Anchor box)

3.Height and width 



Values we are interested in 

Identify the Grid number  say 2,5  out of 13x13 based IOU with the ground truth (Bounding Boxes)

In that grid,locate the centroid (x_c,y_c) which will be the centre of our anchor box

We put a template which will have dimension close to bounding box.

The difference in the width and height of the bounding box and anchor box is something the network has to reduce(error)



