# Task_sphere_NN
**Solving a classification/regression issue. Search for an alternative criterion for better separation of extensive air showers events by primary masses on the data SPHERE-2 experiment.**

**Решение задачи классификации/регрессии. Поиск альтернативного критерия для лучшего разделения событий широких атмосферных ливней по первичным массам на данных эксперимента СФЕРА-2.**


## I Предобработка данных
### Входные данные
Исходные данные событий широких атмосферных ливней смоделированны с помощью программ GEANT4 и CORSIKA. Полученные данные занимают 10 Гб.
Они лежат в архиве на Google Disk: [data_sphere](https://drive.google.com/drive/folders/1XtcPgxcZfs3CUC9Lfm7Dz3P0bNFvn7yW?usp=sharing) в папке mosaic_hits.

### Процесс
Данные для каждой из 10 частиц преобразуются в видеоряд и две карты (карту средних времен активации ФЭУ и карту суммарного числа фотонов в ФЭУ) с помощью программы [Data_sphere_10-20_to_maps](https://github.com/Vetselet/Task_sphere_NN/blob/main/Data_sphere_10-20_to_maps.ipynb).

Необходимо написать верный путь к исходным файлам в переменые: _direct_, _files_p_, _f_coord_.
Программу надо запускать 10 раз для просчета по каждой частице (p, He, N, S, Fe) и двум моделям взаимодействия (q1, q2).

### Выходные данные
Полученные преобразованные данные хранятся в папке на Google Disk: [data_to_NN](https://drive.google.com/drive/folders/1ukIC5x-TCWRd60Hng8-OchCcOwBb8gOr?usp=sharing).


## II Использование нейросети
### Входные данные
В качестве входных данных используются выходные данные первого этапа.

### Процесс
Решение задачи регресси с помощью нейронной сети происходит в програме [Norm_Baseline_NN_sphere_mass_10-20](). 
В главе **"Загрузка данных"** необходимо подставить верные пути директорий в переменные: direct_q1, direct_q2, direct_out_model.

### Выходные данные
Выходной файл [Norm_Baseline_NN_sphere_mass_10-20](https://github.com/Vetselet/Task_sphere_NN/blob/main/Norm_Baseline_NN_sphere_mass_10-20.ipynb) содержит в себе информацию о предсказанной массе частиц (pred), о модельной массе частиц (y) и о смоделированном типе частицы.

P.S. Есть сохраненные веса модели нейронной сети, расположенные в файле [model_weights_5_q1q2.pth](https://github.com/Vetselet/Task_sphere_NN/blob/main/model_weights_5_q1q2.pth).
В программе [Baseline_NN_sphere_mass_10_20.ipynb](https://colab.research.google.com/github/Vetselet/Task_sphere_NN/blob/main/Baseline_NN_sphere_mass_10_20.ipynb) есть вызов сохраненной модели, чтобы не ждать 15 минут просчет нейронной сети.


## III Переход от полученных параметров к усредненной массе частиц
### Входные данные
Полученные данные по регрессии для большого числа событий представляют собой альтернативу классическому критерию, которая необходима для восстановления массы первичной частицы, образовавшей широкий атмосферный ливень.
Выход нейронной сети и истинные типы частиц зафиксированы в таблице [predictions_NN_lnA.csv](https://github.com/Vetselet/Task_sphere_NN/blob/main/predictions_NN_lnA.csv). 

### Процесс
Данные из полученной на II этапе таблицы подаются на вход в программу [method_mass_reconstruction.ipynb](https://github.com/Vetselet/Task_sphere_NN/blob/main/method_mass_reconstruction.ipynb) для восстановления средней массы по выборке событий.

### Выходные данные
Выходными данными являются графики в программе [](), на которых видно, что такой подход позволяет оценить массы первичных частиц.

## Статья

Подробный алгоритм действий и физическое обоснование представлено в статье []().
