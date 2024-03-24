# Task_sphere_NN
**Solving a classification/regression issue. Search for an alternative criterion for better separation of extensive air showers events by primary masses on the data SPHERE-2 experiment.**

**Решение задачи классификации/регрессии. Поиск альтернативного критерия для лучшего разделения событий широких атмосферных ливней по первичным массам на данных эксперимента СФЕРА-2.**

## Предобработка данных

### Входные данные

Существуют исходные данные, полученные в результате моделирования событий широких атмосферных ливней с помощью программ GEANT4 и CORSIKA. Поскольку их объем очень велик, Github не позволяет их внести. Вскоре они будут перенесены на Google Disk.
Исходные данные преобразуются в данные, которые будут поданы на вход нейронной сети, с помощью программы [Data_sphere_10-20_to_maps.ipynb](https://colab.research.google.com/github/Vetselet/Task_sphere_NN/blob/main/Data_sphere_10-20_to_maps.ipynb).

### Выходные данные

Полученные преобразованные данные хранятся в папках на Google Disk: [https://drive.google.com/data_to_NN_q1_900_10PeV_10-20](https://drive.google.com/drive/folders/1Avlm3dYyPC1Rwx6POeY_K8bTmsunCST3?usp=sharing), 
[https://drive.google.com/data_to_NN_q2_900_10PeV_10-20](https://drive.google.com/drive/folders/14b8fn_2X3asCzp-rxP-lPI0b7qsscyz8?usp=sharing).

## Использование нейросети

Предобработанные данные подаются на вход нейронной сети в программе [Baseline_NN_sphere_mass_10_20.ipynb](https://colab.research.google.com/github/Vetselet/Task_sphere_NN/blob/main/Baseline_NN_sphere_mass_10_20.ipynb).

### Выходные данные

Есть сохраненные веса модели нейронной сети, расположенные в файле [model_weights_5_q1q2.pth](https://github.com/Vetselet/Task_sphere_NN/blob/main/model_weights_5_q1q2.pth).
В программе [Baseline_NN_sphere_mass_10_20.ipynb](https://colab.research.google.com/github/Vetselet/Task_sphere_NN/blob/main/Baseline_NN_sphere_mass_10_20.ipynb) есть вызов сохраненной модели.

## Переход от полученных параметров к массе частиц

В результате получается решение задачи регрессии.
Полученные данные о регрессии для большого числа событий представляют собой альтернативу классическому критерию, которая необходима для восстановления массы первичной частицы, образовавшей широкий атмосферный ливень.
Выход нейронной сети и истинные типы частиц зафиксированы в таблице [predictions_NN_lnA.csv](https://github.com/Vetselet/Task_sphere_NN/blob/main/predictions_NN_lnA.csv). 

Данные полученной таблицы подаются на вход в программу [method_mass_reconstruction.ipynb](https://github.com/Vetselet/Task_sphere_NN/blob/main/method_mass_reconstruction.ipynb) для восстановления средней массы по выборке событий.
