# Классификатор эмоций
<br>

![alt text](images/logo.png)

### Описание
<br>
Проект посвящен созданию модели для классификации человеческих эмоций по изображению лица.<br>
В качестве базового фреймворка используется TensorFlow 2.3.0 и Keras.<br>
Обучение проводилось на платформе Google Colab. Эксперименты проводились с 3-мя моделями из **Top-1 Accuracy Keras Applications**:
  
* ResNet50
* VGG16
* Xception
<br>

От базовых моделей "отрезались" финальные (топовые) слои, которые используются для предсказания, они заменялись на слой для предсказания класса эмоций.<br>
Были проведены следующие эксперименты:<br>


| **№ Эксперимента** | **Дата** | **Базовая модель** | **Дополнительные слои**                                                                                                                                                                                                                        | **Оптимизатор**                                            | **Loss**                    | **Аугментация** | **Количество эпох** | **Точность на валидации** |
| ------------------ | -------- | ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- | --------------------------- | ---------------: | -------------------: | -------------------------: |
| 1                  | 19.12.20 | resnet50           | tf.keras.layers.Flatten(),<br>tf.keras.layers.Dense(1024, activation='relu'), tf.keras.layers.Dense(p\_num\_classes, activation='softmax')                                                                                                     | tf.keras.optimizers.SGD(learning\_rate=0.01, momentum=0.9) | 'categorical\_crossentropy' | нет             | 10                  | 34                        |
| 2                  | 22.12.20 | vgg16              | tf.keras.layers.Flatten(),<br>tf.keras.layers.Dense(512, activation='relu'),<br>tf.keras.layers.Dense(p\_num\_classes, activation='softmax')\]                                                                                                 | tf.keras.optimizers.SGD(learning\_rate=0.01, momentum=0.9) | 'categorical\_crossentropy' | нет             | 10                  | 14                        |
| 4                  | 23.12.20 | Xception           | tf.keras.layers.Flatten(),<br>tf.keras.layers.Dense(1024, activation='relu'), tf.keras.layers.Dense(p\_num\_classes, activation='softmax')                                                                                                     | tf.keras.optimizers.SGD(learning\_rate=0.01, momentum=0.9) | 'categorical\_crossentropy' | нет             | 10                  | 34                        |
| 5                  | 24.12.20 | Xception           | tf.keras.layers.Flatten(),<br>tf.keras.layers.Dense(1024, activation='relu'), tf.keras.layers.Dense(p\_num\_classes, activation='softmax')                                                                                                     | tf.keras.optimizers.SGD(learning\_rate=0.01, momentum=0.9) | 'categorical\_crossentropy' | да              | 10                  | 32                        |
| 6                  | 25.12.20 | Xception           | tf.keras.layers.GlobalAveragePooling2D(),<br>tf.keras.layers.Dropout(0.2),<br>tf.keras.layers.Dense(p\_num\_classes, activation='softmax')                                                                                                     | tf.keras.optimizers.Adam(learning\_rate=0.001)             | 'categorical\_crossentropy' | да              | 10                  | 31                        |
| 7                  | 27.12.20 | Xception           | tf.keras.layers.GlobalAveragePooling2D(),<br>tf.keras.layers.Dropout(0.2),<br>tf.keras.layers.Dense(p\_num\_classes, activation='softmax')                                                                                                     | tf.keras.optimizers.Adam(learning\_rate=0.001)             | 'categorical\_crossentropy' | да              | 15                  | 31                        |
| 8                  | 28.12.20 | Xception           | tf.keras.layers.GlobalAveragePooling2D(),<br>tf.keras.layers.Dropout(0.5),<br>tf.keras.layers.Dense(512, activation='relu'),<br>tf.keras.layers.Dense(128, activation='relu'),<br>tf.keras.layers.Dense(p\_num\_classes, activation='softmax') | tf.keras.optimizers.Adam(learning\_rate=0.01)              | 'categorical\_crossentropy' | да              | 17                  | 26                        |
| 9                  | 30.12.20 | Xception           | tf.keras.layers.GlobalAveragePooling2D(),<br>tf.keras.layers.Dropout(0.2),<br>tf.keras.layers.Dense(1024, activation='relu'),<br>tf.keras.layers.Dense(p\_num\_classes, activation='softmax')                                                  | tf.keras.optimizers.SGD(learning\_rate=0.01, momentum=0.9) | 'categorical\_crossentropy' | да              | 20                  | 34                        |
| 10                 | 03.01.21 | resnet50           | f.keras.layers.GlobalAveragePooling2D(),<br>tf.keras.layers.Dropout(0.2),<br>tf.keras.layers.Dense(1024, activation='relu'),<br>tf.keras.layers.Dense(p\_num\_classes, activation='softmax')                                                   | tf.keras.optimizers.SGD(learning\_rate=0.01, momentum=0.9) | 'categorical\_crossentropy' | да              | 20                  | 33                        |
| 11                 | 04.01.21 | resnet50           | f.keras.layers.GlobalAveragePooling2D(),<br>tf.keras.layers.Dropout(0.2),<br>tf.keras.layers.Dense(1024, activation='relu'),<br>tf.keras.layers.Dense(p\_num\_classes, activation='softmax')                                                   | tf.keras.optimizers.SGD(learning\_rate=0.01, momentum=0.9) | 'categorical\_crossentropy' | да              | 40                  | 34                        |
| 12                 | 05.01.21 | resnet50           | Разморожены слои из блока «conv5» базовой модели<br>tf.keras.layers.GlobalAveragePooling2D(),<br>tf.keras.layers.Dense(p\_num\_classes, activation='softmax')                                                                                  | tf.keras.optimizers.SGD(learning\_rate=0.01, momentum=0.9) | 'categorical\_crossentropy' | да              | 20                  | 44                        |
| 13                 | 06.01.21 | Xception           | Разморожены слои из блока «block14» базовой модели<br>tf.keras.layers.GlobalAveragePooling2D(),<br>tf.keras.layers.Dense(p\_num\_classes, activation='softmax')                                                                                | tf.keras.optimizers.SGD(learning\_rate=0.01, momentum=0.9) | 'categorical\_crossentropy' | да              | 20                  | 44                        |
| 14                 | 19.01.21 | Xception           | Все слои модели Xception обучаемы<br>tf.keras.layers.GlobalAveragePooling2D(),<br>tf.keras.layers.Dense(p\_num\_classes, activation='softmax')                                                                                                 | tf.keras.optimizers.SGD(learning\_rate=0.01, momentum=0.9) | 'categorical\_crossentropy' | да              | 20                  | 52                        |
| 15                 | 20.01.21 | resnet50           | Все слои модели Resnet обучаемы<br>tf.keras.layers.GlobalAveragePooling2D(),<br>tf.keras.layers.Dense(p\_num\_classes, activation='softmax')                                                                                                   | tf.keras.optimizers.SGD(learning\_rate=0.01, momentum=0.9) | 'categorical\_crossentropy' | да              | 20                  | 53                        |




Лучший результат: **53%** точности на валидации показали классификаторы на базе **ResNet50** и **Xception**.<br> 
Для модели классификатора применялся оптимизатор *optimizer= tf.keras.optimizers.SGD(learning_rate=0.01, momentum=0.9)*.<br>
Модель обучалась 20 эпох.<br>

При обучении к данным применялась аугментация «на лету» со следующими параметрами:

* horizontal_flip=True,
* zoom_range=0.2,
* height_shift_range=0.2,
* width_shift_range=0.2,
* rotation_range=15
<br><br>

![alt text](model/emo_classificator_best_210120045559_resnet50_e20_aug1_acc53.png)

*Кривая обучения классификатора на базе ResNet50 (лучшее значение получено на 14-й эпохе)*

![alt text](model/emo_classificator_best_210119123752_xception_e20_aug1_acc52.png)

*Кривая обучения классификатора на базе Xception (лучшее значение получено на 9-й эпохе)*

### Заключение

Результаты у классифкаторов на базе **ResNet50** и **Xception** практически одинаковые, поэтому нет разницы, какой из них использовать. Классификатор на базе **VGG16** обучить не удалось, максимальная точность составила всего **14%**, классификатор практически не обучался. Возможно для работы с моделью на базе архитектуры VGG16 нужен другой подход.


### Структура проекта

      data/                               исходные и тестовые данные, словари
      model/                              сохраненные модели по результатом каждого эксперимента
      images/                             картинки для описания проекта
      emo_classificator_model.py          скрипт с классом классификатора эмоций
      emo_classificator_prep_data.ipynb   ноутбук для подготовки аугментированного набора данных для обучения классификатора эмоций
      emo_classificator_test.ipynb        ноутбук для проверки и тестирования классификатора эмоций
      emo_classificator_train.ipynb       ноутбук для создания и обучения классификатора эмоций
      emo_detector_test.ipynb             ноутбук для демонстрации детекции эмоций по видео с камеры в реальном времени
      emo_detector.py                     скрипт с классом детекции эмоций по видео с камеры в реальном времени
      emo_detector.conf                   настройки класса детекции эмоций
      emo_utils.py                        скрипт с базовыми функциями
      experiments.xls                     таблица с описанием проведенных экспериментов 

### Запуск

1. Скачайте исходный набор данных: https://drive.google.com/uc?id=1pm86O0t_0caQq3b3Qz5iNI3T77p2o-C1
2. Распакуйте в папку **data**, в итоге должна получиться следующая структура:

|-data<br>
&nbsp;&nbsp;&nbsp;|---train<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|---anger<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|---...<br>

3. Для обучения классификатора эмоций выполните код из ноутбука **emo_classificator_train.ipynb**, настроив параметры стреды и обучения:

![alt text](images/google_param.png)
![alt text](images/train_params.png)

4. Не обязательно. Для ускорения обучения можно предварительно сгенерироровать аугментированный набор данных. Для этого выполните код из ноутбука **emo_classificator_prep_data.ipynb**

5. Для теста классификатора эмоций используйте ноутбук **emo_classificator_test.ipynb**,  в качестве параметра задайте путь к сохраненной модели из папки models. Скачайте сохраненные модели: https://drive.google.com/drive/folders/1EdXlwE0EBXLMi18fwFKxCX3MuR1sNvay?usp=sharing и распакуйте в папку **model**

6. Для теста детекции эмоций по видео с камеры в реальном времени используйте ноутбук **emo_detector_test.ipynb**, в качестве параметра задайте путь к сохраненной модели из папки models (аналогично п.4).

![alt text](images/emo_detector.png)

