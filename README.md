# car_classification_neural_networks
An example of car classification on a small dataset based on a convolutional neural network

Ссылка на соревнование на Kaggle https://www.kaggle.com/competitions/sf-dl-car-classification

Ссылка на датасет https://www.kaggle.com/competitions/sf-dl-car-classification/data


Целью проекта являлась классификация изображения автомобилей на несколько классов.
В процессе работы над проектом было проверены разные варианты параметров, но, к сожалению,сводную таблицу я предоставить не могу, так как организация экспериментов была несколько хаотичной.
Так же попыталась учесть общие замечания к учебным проектам, обилие которых встречалось в репозитории с отзывами.
Теперь кратко по пунктам. 
1. Я попробовала трансфер-learning как с постепенной разморозкой весов, так и с единоразовой. Особой разницы не заметила по метрикам(по длительности обучения, конечно, разница есть), но из-за ограниченности ресурсов решила использовать единовременную разморозку весов и сделать акцент на обучении головы, так как основной прирост метрики был за счет качества головы. 
2.LR оставила дефолтное, пробовала уменьшать и тогда с применением ReduceLR нейросетка радостно тусила на одном месте в течении десятка эпох.
3.optimizer тоже оставила Adam  как некий усредненный вариант неплохого стохастического градиентного спуска. 
4. Голову сделала максимально простой, и да, в качестве она не сильно ухудшилась после этого(Сравниваю с теми результатами,что были у меня)
Размер картинки пробовала увеличивать до 420, но у меня нет ресурсов,чтобы обучать нейросетку на таком размере картинок:( А колаб про в Россию еще не завезли.
Батч нормализейшен добавляла в состав головы, когда не использовала файнтьюнинг и обучала выходной слой сразу вместе с весами имадженета. Тогда его использование давало небольшой прирост к метрикам.
Коллбэкс функции смотрела в Керас, остановила свой выбор на использовании трех из них.ReduceLR в итоге пригодился, что радует.
Плохо разобралась с ТТА, с его использованием предсказание в сабмите упало до 56 процентов.Что-то явно пошло не так, но что именно, не знаю. Колво шагов достаточно большое-10.
Другие модели нейросетей не стала использовать, так как ресурсы были ограничены и времени на эксперименты особо не осталось. Поэтому я решила поиграть с исходной моделькой, но я видела,что многие юзают EfficientNet и достигают хороших результов в метриках.
Библиотеку albumentations  в самом начале пробовала потрогать,но это было так медленно и столько ресурсов лопало,что я эту идею отбросила.
Также я пробовала нормализацию, предназначенную для модели Xception и имеющуюся в модуле, но я не разобралась, куда ее применять. Когда я применяла ее вместо параметра 
1./255, вылетала ошибка несоответствия numpy-array на результате ожидавшемуся, размерность не совпадала. Так же многие в отзывах на работы студентов спрашивают,что за 
1./255. Оно приводится в бейзлайне для этой модели, а составитель оного периспользовал его из статьи на Хабре, вероятно. https://habr.com/ru/post/347564/ 

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
