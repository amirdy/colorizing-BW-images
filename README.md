<ins>[Preview](#preview)</ins>&nbsp;&nbsp;&nbsp;
<ins>[Details of Implementation](#Details-of-Implementation)</ins>&nbsp;&nbsp;&nbsp;
<ins>[Network](#Network)</ins>&nbsp;&nbsp;&nbsp;
<ins>[Hyperparameters and Tools](#Hyperparameters-and-Tools)</ins>&nbsp;&nbsp;&nbsp;
<ins>[Results](#Results)</ins>&nbsp;&nbsp;&nbsp;
<ins>[References](#References)</ins>&nbsp;&nbsp;&nbsp;
<ins>[Useful Resources](#Useful-Resources)</ins>&nbsp;&nbsp;&nbsp;
# Preview

# Details of Implementation

## Dataset 

This dataset consists of about **5,000** of people images including family portrait, wedding portrait and so on:
- [The Images of Groups Dataset (Cornel University)](http://chenlab.ece.cornell.edu/people/Andy/ImagesOfGroups.html)

The images have not a same dimensions and the average dimension of images is : 

## Preprocessing
1- The Black&White images were removed from the dataset.

2- The dimension of the images was changed to (768 x 768).

3- These RGB color space images were converted to Lab color space images.
  
  - Why?
      In the Lab color space, only the second(b) and third(b) channels control the colorization of the image. thus, for training of the Generator
      the L channel can be ignored. Removing one channel defenitely makes the problem easier.

4- At the end, some sort of normalization was taken:
 - All of the values in L channel first divided by 50 and then minus by 1 
 
 - All of the values in a and b channels divided by 128
 
   (These two steps led to having a 3 dimnetional matrix in which all the values are in the range of [-1,1])
 

# Network
## Generator : 

- ### Input:
  - Batch of image [just channel **L**]
    - A Tensor of shape (\*, 1, 768, 768) 
   
      - \* : Batch Size
    
- ### Output:
  - The predicted values of the channels **a** and **b**
  
    - A Tensor of shape (\*, 2, 768, 768)

- ### Structure:
  - Unet 

    - Encoder : EfficientNet-b5

    - use ImageNet pretrained weights

    - 
    


## Discriminator : 

- ### Input:
  - A Tensor of shape (\*x2, 3+3, 768, 768) 
   

- ### Output:
  - A Tensor of shape (\*2, 1, 94, 94)

- ### Structure:




# Hyperparameters and Tools
- #### Batch size: 
   - 3 
- #### Optimizers: 
   - Generator: ADAM | Learning rate : 0.001
   - Discriminator: ADAM | Learning rate : 0.001

- #### Weight Decay: 
   - 0.0001
- #### Loss: 
   - Cross entropy
- #### Train vs Validation Split: 
   - Approximately : 0.78 | 0.22  
- #### Tools: 
   - Python - Pytorch ( Using Google Colab Pro )




