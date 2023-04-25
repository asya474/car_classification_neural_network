# car_classification_neural_networks
An example of car classification on a small dataset based on a convolutional neural network

Ссылка на соревнование на Kaggle https://www.kaggle.com/competitions/sf-dl-car-classification

Ссылка на датасет https://www.kaggle.com/competitions/sf-dl-car-classification/data

---------------------------------------------------------------------------------------------------------------------------------------------------------------------
The aim of the project was to classify the image of cars into several classes.
In the process of working on the project, various options for the parameters were checked, but, unfortunately, I cannot provide a summary table, since the organization of the experiments was somewhat chaotic.
I also tried to take into account general comments on educational projects, the abundance of which was found in the repository with reviews.
Now briefly on the points.
1. I tried transfer-learning both with a gradual defrosting of the scales and with a one-time one. I didn’t notice much difference in terms of metrics (of course, there is a difference in the duration of training), but due to limited resources, I decided to use a one-time defrosting of the scales and focus on head training, since the main increase in the metric was due to the quality of the head.
2.LR left the default, tried to reduce it, and then, using ReduceLR, the neural network happily hung out in one place for ten epochs.
3.optimizer also left Adam as a kind of average version of a good stochastic gradient descent.
4. I made the head as simple as possible, and yes, it didn’t deteriorate much after that (I compare it with the results that I had)
I tried to increase the size of the picture to 420, but I don’t have the resources to train the neural network on this size of pictures :( And the colab pro has not yet been delivered to Russia.
Butch added normalization to the composition of the head when she did not use finetuning and trained the output layer immediately along with the weights of the imagenet. Then its use gave a small increase to the metrics.
I looked at the function callback in Keras and decided to use three of them. ReduceLR ended up being useful, which is good.
I didn’t deal well with TTA, with its use the prediction in the submission fell to 56 percent. Something obviously went wrong, but I don’t know what exactly. The number of steps is quite large - 10.
I did not use other models of neural networks, since resources were limited and there was not much time left for experiments. Therefore, I decided to play with the original model, but I saw that many people use EfficientNet and achieve good results in metrics.
I tried to touch the albumentations library at the very beginning, but it was so slow and consumed so many resources that I discarded this idea.
