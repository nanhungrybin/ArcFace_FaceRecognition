# Face Recognition using ARCFACE-Pytorch

## Introduction
This repo contains file which is able to perform face recogntion.
#### < arcface_engine_id.py >


## Test Demo Result
![image](https://github.com/nanhungrybin/ArcFace_FaceRecognition/assets/97181397/3985dff7-aa9d-48ef-a373-80edb271b330)

 
## Required Files
- requirements.txt
- pretrained model [IR-SE50 @ Onedrive](https://onedrive.live.com/?authkey=%21AOw5TZL8cWlj10I&cid=CEC0E1F8F0542A13&id=CEC0E1F8F0542A13%21835&parId=root&action=locate) or [Mobilefacenet @ OneDrive](https://onedrive.live.com/?authkey=%21AIweh1IfiuF9vm4&cid=CEC0E1F8F0542A13&id=CEC0E1F8F0542A13%21836&parId=root&o=OneUp).
- Custom dataset
- Newly Trained model (facebank.pth and names.npy)


## User Instruction
After downloading the project first you have to install the following libraries.
### Installation
You can install all the dependencies at once by running the following command from your terminal.
``` python
    $ pip install -r requirements.txt
```
##### For the installation of torch using "pip" run the following command

``` python
    $ pip3 install torch===1.2.0 torchvision===0.4.0 -f https://download.pytorch.org/whl/torch_stable.html
```
### Project Setup

#### pre-trained model
Although i provided the pretrained model in the <b> work_space/model </b> and <b> work_space/save </b> folder, if you want to download the models you can follow the following url:

- [IR-SE50 @ BaiduNetdisk](https://pan.baidu.com/s/12BUjjwy1uUTEF9HCx5qvoQ)
- [IR-SE50 @ Onedrive](https://onedrive.live.com/?authkey=%21AOw5TZL8cWlj10I&cid=CEC0E1F8F0542A13&id=CEC0E1F8F0542A13%21835&parId=root&action=locate)
- [Mobilefacenet @ BaiduNetDisk](https://pan.baidu.com/s/1hqNNkcAjQOSxUjofboN6qg)
- [Mobilefacenet @ OneDrive](https://onedrive.live.com/?authkey=%21AIweh1IfiuF9vm4&cid=CEC0E1F8F0542A13&id=CEC0E1F8F0542A13%21836&parId=root&o=OneUp)

I have used the <b>IR-SE50</b> as the pretrained model to train with my custom dataset. You need to copy the pretrained model and save it under the <b> work_space/save </b> folder as <b> model_final.pth</b>

#### Newly trained model
In the <b> data/facebank </b> you will find a trained model named <b> "facebank.pth" </b> which contains the related weights and "names.npy" contains the corresponding labels of the users that are avialable in the facebank folder. For instance in this case
the <b> facebank </b> folder will look like this :-

    facebank/
                ---> Chandler
                ---> Joey
                ---> Monica
                ---> Phoebe
                ---> Pias
                ---> Rachel
                ---> Raihan
                ---> Ross
                ---> Samiur
                ---> Shakil
                ---> facebank.pth
                ---> names.npy

If you have the "facebank.pth" and "names.npy" files in the <b>data/facebank</b> you can execute the following command to see the demo.




#### Dataset preparation 

First organize your images within the following manner- 

    data/
        raw/
             name1/
                 photo1.jpg
                 photo2.jpg
                 ...
             name2/
                 photo1.jpg
                 photo2.jpg
                 ...
             .....
now run the following command
```python
$ python .\create-dataset\align_dataset_mtcnn.py data/raw/ data/processed --image_size 112
```

You will see a new folder inside the data directory named <b> "processed" </b> which will hold all the images that contains only faces of each user. If more than 1 image appears in any folder for a person, average embedding will be calculated. 

After executing the script new images for each user in the processed folder will look something like this.
<p align="center"> 
<b> Cropped Images of faces </b>
    <img src ="http://muizzer07.pythonanywhere.com/media/files/Picture1.png">
</p> 

Copy all the folders of the users under the <b>data/processed</b> folder and paste in the <b>data/facebank</b> folder.


Now to train with your dataset, you need to set <b> args.update == True </b> in line 35 of face_verify.py . After training you will get a new facebank.pth and names.npy in your data/facebank folder which will now only holds the weights and labels of your newly trained dataset. Once the training is done you need to reset <b> args.update==False</b>.
However, if this doesn't work change the code in following manner-

## References
- [Arcface](https://arxiv.org/pdf/1801.07698.pdf)
- [InsightFace_Pytorch](https://github.com/TreB1eN/InsightFace_Pytorch)
- [The one with Face Recognition.](https://towardsdatascience.com/s01e01-3eb397d458d)
