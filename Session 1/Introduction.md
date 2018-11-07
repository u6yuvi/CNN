# EIP-Session1 -Assignment                                               

![Image result for cnn convolution](https://cdn-images-1.medium.com/max/1600/1*EPpYI-llkbtwHgfprtTJzw.png)



- ## **<u>Convolution</u>**

Convolution is an operation done  to extract features from the images as these features will be used by the network to learn about a particular image.In the case of a dog image,the feature could be the shape of a nose or the shape of an eye which will help the network later to identify an image as a dog.

Convolution operation is performed with the help of the following three elements:

1.Image-The image to convolve on

2.Feature Detector or a Kernel-They are the bunch of numbers in a matrix form intended to extract features from an image.They can be 1dimensional ,2-dimensional or 3-dimensional

3.Feature Map-The resultant of the convolution operation performed between image and feature detector gives a Feature Map.

How do they all fit together?

In 2-d convolution

We convolve between feature detector(bunch of number in a matrix form of size )
$$
f(h)*f(w)
$$
 and the image of size 
$$
n(h)*n(w)
$$
 to get a new matrix which is called feature map.

n(h)-height of the image

n(w)-width of the image

f(h)-height of the filter

f(w)-width of the filter

In case of a square filter f(h)=f(w)

In 3-d convolution-**Convolution over volume**

In the case of image with multiple channels like an RGB image,the image is represented by 
$$
n(h)*n(w)*n(c)
$$
where n(c) is the number of channel in the image.

Say we have a 7x7x3 image and we convolve this image using a feature detector of 3x3x3 then the result of the convolution will be a 2 dimensional feature map of  shape 5x5.Like this we can use multiple feature detectors(kernels) to extract multiple features from an image and the stack of these kernels constitute one layer in Convolution Neural network Architecure.

Things to remember

Feature detector will always have the same number of channel as the image.

Convolving gives a 2 dimensional feature map although our image and feature detector used are of 3 dimensional

A general way to represent it would be:
$$
n(h)*n(w)*n(c)--convolvewith--[f(h)*f(w)*n(c)],n(c')--willresultinto--(n-f+1)*(n-f+1)*n(c')
$$
where n(c') represents the number of such filters used.



- ## **Filter/Kernels**

Filters/Kernels are a bunch of numbers which when convolved over image extracts a particular feature of the image.The feature could be edges,lines etc in the image.

Earlier,before the era of neural networks,the researchers use to design these feature kernels with the numbers that represented what kind of features they are intended to extract from an image.

For eg:

![1537807515391](C:\Users\u6yuv\AppData\Roaming\Typora\typora-user-images\1537807515391.png) 

This 3x3 kernal was intended to detect the presence of lines of a particular width at a particular orientation.

However,now with neural network ,we now do not need to use specific feature detector intended for specific feature extraction,rather we initialize it with random numbers and then neural network through backpropagation does the cool work to come up with the right feature detectors.



- ## <u>**Epochs**</u>

It is the number of times the network  sees all the data in our dataset.This technique can be thought of as simulation process,where we are making the neural network to see all the data again and again till the time the network does not start making the right prediction on the data.

Few things to note:

1. Greater the number of epocs higher will be the training time.

2. Greater the number of epocs will generally offer a better accuracy but up to a certain point.After that the model starts overfitting.We can observe that in the below image:

   ![1538113005612](C:\Users\u6yuv\AppData\Roaming\Typora\typora-user-images\1538113005612.png)

After 8th epoch,the model started overfitting.



- ## <u>**1x1 convolution**</u>

At first,the idea of using 1x1 filter to convolve over image seems to not make sense as  1x1 convolution is working like a coordinate dependent transformation in the filter space by just multiplying  by numbers in particular coordinate and this will not lead to learning any feature.

But wait... What if we have a layer with dimension 32x32x196,here 196 is the number of channels.

So 1x1x192 convolution will do the work of dimensionality reduction by looking at each of the 196 different positions  and it will do the element wise product and give out one number.Hence the dimensionality reduces from32x32x196 to 32x32x1.

A good intuitive understanding of 1x1 convolution which does sum pooling of features across various channels/feature-maps of a given layer is to consider it like a DJ which mixes and matches different features of multiple songs(kernels) into one.

When to use 1x1 filter

1. 1x 1 filter can be used in shrinking the number of channels or increasing the number of channels without changing the height and width of the layer.

2. When we want to build deeper network without simply stacking more layers.It is like going wide(by replacing few filters with a mixture of 1x1 and 3x3 convolutions) instead of going deep.The implementation can be found under Inception Module used in GoogLeNet architecture.

3. To add more non-linearity in the network.

   Generally 1x1 convolution is followed by non linear activation layer like ReLU .So adding many 1x1 convolution does not hurt much to the network as it avoids overfitting due to smaller kernel size.



- ## <u>**3x3 convolution**</u> 

3x3 convolution  involves the use of 3x3 filter(feature detector) which is convolved over an image.

The operation involves  element wise multiplication of 9 number of the filter matrix (which are the learning parameters) and the image pixel which is later added to get a single number while the filter moves in 2-direction(x,y) over an image.

Use of 3x3 filter reduces the resolution of the image by 2 units.

Say if we have an image of 28x28x3  and we apply a convolution between this image and a feature detector,the end result is a feature map of size 26x26,which is a reduction of resolution by unit 2. 



- ## <u>**Feature Maps**</u>     

An simple way to understand Feature Map is ,it does the work of storing the feature which we find by convolving  a feature detector over an image.

Hidden layers in Convolution Neural Network is the stack of feature maps.A unit in a feature map is connected to different units in the lower layer(layer farthest from prediction).In the case of the first hidden layer,the units within the feature map is connected to different regions of the input range and this range is determined by the size of the feature detector used.

Lets take an example and understand:

Say you have an image of a bicycle and we use a network of 3 hidden layers.

The feature maps in  the first hidden layer will try to capture the high level features which could be curves in the bicycle.In the second layer,as the feature map of this layer is looking into the features reported on the first layer feature map,it could look at a combination of curves that build circles.The feature map in the third  layer will capture features built over the previous layer's feature maps like it could detect a bicycle from lines and circle .





- ## <u>**Feature Engineering **</u>

The idea of feature engineering is a bit older concept now where the idea was to manually engineer features to detect from an image.Features are nothing but a vector of real numbers .Hand curated Feature detectors were the tools to extract features from an image.But now the idea is to automatically learn a set of features from, potentially noisy, raw data in solving certain tasks such as image recognition,object detection etc.

# **<u>Additional Topics</u>**



- ## <u>**Activation**</u>

What makes neural network outperform every other machine learning model is that it can learn  very complex non linear relationships in the data.The one biggest factor is the use of activation functions which does non linear transformations to the inputs received to a neuron from preceding layer neurons .Neural Network without an activation function is just a bunch of linear regression models which takes all the inputs and do a linear transformations.In that case the network will not be able to perform complex tasks. 

A good analogy that I would I like to draw here is:

Consider a scenario where three applicants (Applicant A, Applicant B and Applicant C) reach out to bank to get a loan.Each one of them submitted the loan form that has a reason to lend money.However Bank eventually decided to approve applicant C loan form and forwarded that form to loan disbursement department 

Now lets fit this scenario in neural network to understand what activation means



![1538144872998](C:\Users\u6yuv\AppData\Roaming\Typora\typora-user-images\1538144872998.png)





Consider Bank as a neuron

Applicant as the bunch of numbers coming to this neuron from the previous layer neurons

Heuristic used by a Bank as activation function  that just allows applicant C  form to pass.

So you can think of  activation function as the brain of neuron which decides on what numbers this neuron can allow to pass through it to pass on to the next layer.

Different activation functions that can be found in research papers are the following:

1.Binary Step Function

2.ReLU

3.Leaky Relu

4.ELu

5.Sigmoid

6.tanh

7.Softmax

Amongst all Relu has been the one which is widely used in the hidden layers and softmax at the output layer.



- ## <u>**Receptive Fields**</u>


Receptive filed is an area in the input image that a particular CNN's feature is affected by.Unlike feed forward network where each neuron at a particular layer receives connections from all neurons in the previous layer, CNNs use a receptive field-like layout in which each neuron(feature) receives connections only from a subset of neurons(features) in the previous (lower) layer. As we go towards higher layers in the network,the higher layer neurons looks at a combination of receptive fields( i.e. larger portion of the image) from several (but not all) neurons in the layer before. In this way, each successive layer tries to learn  abstract features with the help of basic/low level features learned at a lower layer .

A good analogy will be to think CNN network as any Company hierarchical structure.

![1538113372026](C:\Users\u6yuv\AppData\Roaming\Typora\typora-user-images\1538113372026.png)



President at the top layer is not connected directly with the bottom level departments,but yet,it knows what is happening where through interacting with people just below his/her layer which further interacts with people below them and this continues this the bottom layer.In this way,we can say a President is indirectly looking at all the work of bottom layer and this is the receptive field of the President.

The wider the President can connect and be in control  with the bottom layer,the bigger its receptive field will be.



- ## How to create an account on GitHub and upload a sample project

**Starting with Git**

In this article we will learn how to setup a Git repository ,add files to the repository,make commits and finally make this repository public by putting it on Github.

You must have heard of Git repository.But what makes a repository a Git repository?

It is as similar to a folder which you have on your computer,the only thing which makes it a git repository is it stores the metadata of the history of the folder in a .git directory  which is present in the directory but hidden.

Without further ado lets make a git repository but before that make sure you install git on your computer.

Download git from this link: [Git](https://git-scm.com/downloads)

There are two ways to do it.

1.Either you have a folder where you have bunch of files and you want that folder to become a Git repository.

Go to that folder on git and type git init.

It adds a .git file to the folder and Voila !! it is now a git repository.

2.You are starting afresh and want to initialize a repository where you will start putting up your work.

As we are starting afresh,we shall go with the 2^nd^ approach 

Steps which I followed are the following:

1.Open git bash.

1.Create a new folder named **git_example** using mkdir 

2.Changed my director to **git_example** through cd(change directory)

3.Make sure we don't have any file inside this folder through command **ls -a**(shows normal as well as hidden files)

4.Initialized this folder as a git repository by **git init**

5.Doing **ls -a** to make sure it is now a git repository ( .git file(hidden file) appeared inside the folder).

![1537886716983](C:\Users\u6yuv\AppData\Roaming\Typora\typora-user-images\1537886716983.png)

Anytime we can check the status of our repository by typing **git status**:

![1537887522094](C:\Users\u6yuv\AppData\Roaming\Typora\typora-user-images\1537887522094.png)

It provides a bunch of information:

1.We are in the master branch

2.We have not done any commit yet



Now lets add our first .txt file file in this directory

![1537888132957](C:\Users\u6yuv\AppData\Roaming\Typora\typora-user-images\1537888132957.png)

It opens a notepad with a new text file.

![1537888216618](C:\Users\u6yuv\AppData\Roaming\Typora\typora-user-images\1537888216618.png)

Add the text in the file and close it.

Now if you do **ls** we will see ex1.txt file created.

We can also check the repository status here by typing **git status**

![1537888348050](C:\Users\u6yuv\AppData\Roaming\Typora\typora-user-images\1537888348050.png)We can see   that now  **ex1.txt** file is listed as untracked files.

Now I would like to encourage you to create one more file using the same steps we followed above.

Once you are done,do **git status**,you will now find two files under untracked file.

![1537890251774](C:\Users\u6yuv\AppData\Roaming\Typora\typora-user-images\1537890251774.png)

# **Staging Area**

![1537889917662](C:\Users\u6yuv\AppData\Roaming\Typora\typora-user-images\1537889917662.png)

Consider a scenario where you are writing code to build a new features on a product.These two files which we added earlier contains the codes for the new feature.You finished up  coding for 1st file and would like to commit.

Git provides an intermediate directory called staging directory which is Git way of saying "Hey here is the cache where you can put all your  files which are finely prepared to commit. "

So lets go ahead and add ex1.txt file to staging directory

![1537890929401](C:\Users\u6yuv\AppData\Roaming\Typora\typora-user-images\1537890929401.png)

W can see our ex1.txt file is in the staging area which is why it is marked as **Changes to be commited**

and our **ex2.txt** file is still untracked.



*Note-If you accidentally added file to staging area,you can remove it using **git reset**.*

Now we are about to make our first commit .When we do this we need to write a message describing our changes.

We can add commit message in two ways:

1.Use **git commit**.It will open the editor where you can add your commit message.

2.Using command line via  **git commit -m "commit message"**.

Lets go ahead and make our first commit.

![1537891502458](C:\Users\u6yuv\AppData\Roaming\Typora\typora-user-images\1537891502458.png)

*Refer this [this style guide](http://udacity.github.io/git-styleguide/) describes some common best practices when writing commit messages.*

We can use **git log** to see the commit has been created.Here it is..

![1537892268507](C:\Users\u6yuv\AppData\Roaming\Typora\typora-user-images\1537892268507.png)



Do git status and see the changes

![1537892434954](C:\Users\u6yuv\AppData\Roaming\Typora\typora-user-images\1537892434954.png)

The initial commit note has gone away and the only remaining untracked file is ex2.txt.

You can go ahead and commit ex2.txt in the same way we did for ex1.txt.

Once you done with commit,the result of git status will be we having nothing else to commit.

![1537892596162](C:\Users\u6yuv\AppData\Roaming\Typora\typora-user-images\1537892596162.png)

We have nothing to commit.



Now lets make some changes in our ex1.txt and ex2.txt.

I am adding a new line of text in each file. 

![1537893539391](C:\Users\u6yuv\AppData\Roaming\Typora\typora-user-images\1537893539391.png)

Now lets do **git status**

![1537893617731](C:\Users\u6yuv\AppData\Roaming\Typora\typora-user-images\1537893617731.png)

As we modified these two files,we can see them tagged as modified.



Lets take a step back and think about what  working directory,staging directory and Repository looks like right now:

Repository generally consist of several commits and each commits consist of several files.As till now we just did commit once so it contains 1 commit which has ex1.txt and ex2.txt .

Staging area is the copy of most recent commit untill we add changes to it.So right now it has the same files as in repository.

Finally working directory also has the same files as we have in staging directory and repository but we have made changes in the ex1.txt and ex2.txt .

![1537894490956](C:\Users\u6yuv\AppData\Roaming\Typora\typora-user-images\1537894490956.png)

Denoting changed file through *



Now to compare between working directory and staging directory,we will use **git diff**

![1537894590131](C:\Users\u6yuv\AppData\Roaming\Typora\typora-user-images\1537894590131.png)

text in green shows the changes that I did.

Now we will go ahead and commit these changes to the repository 

![1537895049584](C:\Users\u6yuv\AppData\Roaming\Typora\typora-user-images\1537895049584.png)

Doing **git log** will give the following details:

![1537895111948](C:\Users\u6yuv\AppData\Roaming\Typora\typora-user-images\1537895111948.png)

We can see the list of commits that we did till now.

To compare two commits in repository  use **git diff commit_id1 commit_id2**

![1537895559370](C:\Users\u6yuv\AppData\Roaming\Typora\typora-user-images\1537895559370.png)

To compare between  staging area and most recent commit do **git diff --staged**.



Github 

Now how can we share this work of ours with someone else?

Here enters the Github

It is a website that allows us to share entire git repository to people.

Go ahead and create a Github account using this link: [Github]( https://github.com/)



Once you are in your account use **+** sign to create a new repository.

![1537984525463](C:\Users\u6yuv\AppData\Roaming\Typora\typora-user-images\1537984525463.png)



If I were making a repository on Github before I had created any content then I would check this README box because that way my repository will start out with 1 commit in it.

*Note-You cannot clone a repository with 0 commit.*

But since I already had commits in my repository that I want to share I won't check this box.

Once you create your repository it will take you to this page:

![1537984852827](C:\Users\u6yuv\AppData\Roaming\Typora\typora-user-images\1537984852827.png)

W ewill be using the https link to add this repository as a remote to our local repository on our computer.

Lets get back to Git

Run **git remote**

It will show all the configured remotes till now.As we have not configured yet it will show none.

Run **git remote add origin** **<paste the https link here>**

As we have just one remote for this repository ,I am naming it as origin

![1537985068763](C:\Users\u6yuv\AppData\Roaming\Typora\typora-user-images\1537985068763.png)

We can see now origin remote has been created.

To check you entered the right https link we can do

**git remote -v**

![1537985143593](C:\Users\u6yuv\AppData\Roaming\Typora\typora-user-images\1537985143593.png)

The output shows both the url from where we will fetch the data from and push the data to.

Now lets push the local repository to Github using the command

**git push origin master**

By default all our files are under master branch.We can create multiple branches and push accordingly.

You can refer this link to understanding What a Branch is

[Branch in Git](https://git-scm.com/book/en/v1/Git-Branching-What-a-Branch-Is)

![1537985390074](C:\Users\u6yuv\AppData\Roaming\Typora\typora-user-images\1537985390074.png) 

Voila!!! We successfully sent our repository on Github.

Refresh the Github page and you will find all your files under the Git tutorial Repository.

![1537985509308](C:\Users\u6yuv\AppData\Roaming\Typora\typora-user-images\1537985509308.png)

You can notice there are 3 commits in this repository which is inline with the commits that we did in our local repository.

That is all for now. Thanks!