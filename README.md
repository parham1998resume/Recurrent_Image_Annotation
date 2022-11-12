# Recurrent_Image_Annotation
Implementation of some popular Recurrent Image Annotation papers on Corel-5k dataset with PyTorch library

## Dataset
<div align="justify"> There is a 'Corel-5k' folder that contains the (Corel-5k) dataset with 5000 images, which has 260 labels in the vocabulary. </div>

(for more information see [CNN_Image_Annotation_dataset](https://github.com/parham1998/CNN_Image_Annotaion#dataset))

## Long short-term memory (LSTM) 
![0](https://user-images.githubusercontent.com/85555218/138563103-f02523b5-f2b7-4a1b-99a7-b448d9d2d031.png)

**Performance of LSTM in one time step:**

![1](https://user-images.githubusercontent.com/85555218/138563233-703a5348-751d-4b04-ba5a-c8e743dfc65f.gif)
![2](https://user-images.githubusercontent.com/85555218/138563236-2c11bad0-b7d2-4ac3-87cf-4fd59112a870.gif)
![3](https://user-images.githubusercontent.com/85555218/138563237-885b3ac9-b0af-48b3-8f37-4ef80959f006.gif)
![4](https://user-images.githubusercontent.com/85555218/138563238-517344f7-b653-42ca-b831-30a28398c16d.gif)

## Convolutional neural network (CNN) 
<div align="justify"> As compared to other CNNs in my experiments, TResNet produced the best results for extracting features of images, so it has been chosen as the feature extractor. </div>

(more information can be found at [CNN_Image_Annotation_convolutional_models](https://github.com/parham1998/CNN_Image_Annotaion#convolutional-models))

## CNN+LSTM models
<div align="justify"> 
1) RIA: <br >
RIA is an encoder-decoder model that uses CNN as an encoder and LSTM as a decoder. In the training phase, it is trained using training images and human annotations. During the test phase, the RIA model predicts the first output label after receiving the input image and being triggered by the <b>start</b> signal. Using the previous output as input for the next time step, it predicts the tag sequence recursively. The loop will continue until the <b>stop</b> signal is predicted. Its structure for the test phase is shown in the images below: </div>

![RIA](https://user-images.githubusercontent.com/85555218/201467303-9f61fb86-0389-43a4-9d1b-e0ced7e592b2.jpg)
<div align="justify"> The labels are mapped to embedding vectors by using lookup tables instead of one-hot vectors. The lookup table can be trained and learn what kind of representation to generate. However, experiments have shown that using pre-trained weights like the GloVe embedding weights provide better results. </div>

## Evaluation Metrics
<div align="justify"> Precision, Recall, F1-score, and N+ are the most popular metrics for evaluating different models in image annotation tasks.
I've used per-class (per-label) and per-image (overall) precision, recall, f1-score, and also N+ which are common in image annotation papers. </div>

(check out [CNN_Image_Annotation_evaluation_metrics](https://github.com/parham1998/CNN_Image_Annotaion#evaluation-metrics) for more information)

## Train and Evaluation

## Results
<div align="justify"> 1) RIA: </div>

| batch-size | num of training images | image-size | epoch time | GloVe weights | image embedding dim | label embedding dim 
| :------------: | :------------: | :------------: | :------------: | :------------: | :------------: | :------------: |
| 32 | 4500 | 448 * 448 | 140s | True | 2048 | 300 |
  
| data | precision | recall | f1-score |
| :------------: | :------------: | :------------: | :------------: |
| *testset* per-image metrics | 0.633  | 0.630 | 0.631 | 
| *testset* per-class metrics | 0.412 | 0.436 | **0.423** |

| data | N+ |
| :------------: | :------------: |
| *testset* | 157 |

## Conclusions

## References
J. Jin, and H. Nakayama. <br />
*"Recurrent Image Annotator for Arbitrary Length Image Tagging"* (ICPR-2016)

F. Liu, T. Xiang, T. M Hospedales, W. Yang, and C. Sun. <br />
*"Semantic Regularisation for Recurrent Image Annotation"* (CVPR-2017)

A. Dutta, Y. Verma, and C.V. Jawahar. <br />
*"Recurrent Image Annotation With Explicit Inter-Label Dependencies"* (ECCV-2020)
