# Task_sphere_NN
**Solving a classification/regression issue. Search for an alternative criterion for better separation of extensive air showers events by primary masses on the data SPHERE-2 experiment.**

**Решение задачи классификации/регрессии. Поиск альтернативного критерия для лучшего разделения событий широких атмосферных ливней по первичным массам на данных эксперимента СФЕРА-2.**


## I Предобработка данных
Первй этап самый длительный по времени из-за большого количества исходных данных, которые в сумме весят 10 Гб. Одно ядро рассчитывается около 30 минут.

### Входные данные
Исходные данные событий широких атмосферных ливней смоделированны с помощью программ GEANT4 и CORSIKA.
Они лежат в архиве на Google Disk: [data_sphere](https://drive.google.com/drive/folders/1XtcPgxcZfs3CUC9Lfm7Dz3P0bNFvn7yW?usp=sharing) в папке mosaic_hits.

### Процесс
Данные для каждой из 10 частиц преобразуются в видеоряд и две карты (карту средних времен активации ФЭУ и карту суммарного числа фотонов в ФЭУ) с помощью программы [Data_sphere_10-20_to_maps](https://github.com/Vetselet/Task_sphere_NN/blob/main/Data_sphere_10-20_to_maps.ipynb).

Необходимо написать верный путь к исходным файлам в переменые: _direct_, _files_p_, _f_coord_.
Программу надо запускать 10 раз для просчета по каждой частице (p, He, N, S, Fe) и двум моделям взаимодействия (q1, q2).

### Выходные данные
Полученные преобразованные данные хранятся в папке на Google Disk: [data_to_NN](https://drive.google.com/drive/folders/1ukIC5x-TCWRd60Hng8-OchCcOwBb8gOr?usp=sharing).


## II Использование нейронной сети
Реализация этого этапа происходит в _google Colab_.

### Задача классификации
#### Входные данные
В качестве входных данных используются выходные данные первого этапа.

#### Процесс
Решение задачи классификации на два и на три ядра с помощью нейронной сети происходит в программах [Baseline_sphere_classification_2core](https://github.com/Vetselet/Task_sphere_NN/blob/main/Baseline_sphere_classification_2core.ipynb) и [Baseline_sphere_classification_3core](https://github.com/Vetselet/Task_sphere_NN/blob/main/Baseline_sphere_classification_3core.ipynb). 
В главе **"Загрузка данных"** необходимо подставить верные пути директорий в переменные: _direct_q1_, _direct_q2_.

#### Выходные данные
В качестве выходных данных выступают графики, которые показывают насколько лучше нейронная сеть лучше разделяет события по сравнению с традиционным методом и с другим экспериментом.

### Задача регрессии
#### Входные данные
В качестве входных данных используются выходные данные первого этапа.

#### Процесс
Решение задачи регресси с помощью нейронной сети происходит в програме [Norm_Baseline_NN_sphere_mass_10-20](https://github.com/Vetselet/Task_sphere_NN/blob/main/Norm_Baseline_NN_sphere_mass_10-20.ipynb). 
В главе **"Загрузка данных"** необходимо подставить верные пути директорий в переменные: _direct_q1_, _direct_q2_, _direct_out_model_.

#### Выходные данные
Выходной файл [predictions_NN_lnA_norm](https://github.com/Vetselet/Task_sphere_NN/blob/main/predictions_NN_lnA_norm.csv) содержит в себе информацию о предсказанной массе частиц (pred), о модельной массе частиц (y) и о смоделированном типе частицы.

P.S. Есть сохраненные веса модели нейронной сети, расположенные в файле [model_weights_5_q1q2](https://github.com/Vetselet/Task_sphere_NN/blob/main/model_weights_5_q1q2_norm.pth).
В программе [Norm_Baseline_NN_sphere_mass_10-20](https://github.com/Vetselet/Task_sphere_NN/blob/main/Norm_Baseline_NN_sphere_mass_10-20.ipynb) есть вызов сохраненной модели, чтобы не ждать 15 минут просчет нейронной сети.


## III Переход от полученных параметров к усредненной массе частиц
### Входные данные
Полученные данные по регрессии для большого числа событий представляют собой альтернативу классическому критерию, которая необходима для восстановления массы первичной частицы, образовавшей широкий атмосферный ливень.
Выход нейронной сети и истинные типы частиц зафиксированы в таблице [predictions_NN_lnA_norm](https://github.com/Vetselet/Task_sphere_NN/blob/main/predictions_NN_lnA_norm.csv). 

### Процесс
Данные из полученной на II этапе таблицы подаются на вход в программу [method_mass_reconstruction](https://github.com/Vetselet/Task_sphere_NN/blob/main/method_mass_reconstruction.ipynb) для восстановления средней массы по выборке событий.

Необходимо написать правильный путь к файлу в переменную _file_predictions_

### Выходные данные
Выходными данными являются графики в программе [method_mass_reconstruction](https://github.com/Vetselet/Task_sphere_NN/blob/main/method_mass_reconstruction.ipynb), на которых видно, что такой подход позволяет оценить среднюю массу по выборкам с точностью 1.17 а.е.м.

## Традиционный метод оценки средних масс
Расчеты, связанные с традиционным критерием можно посмотреть на странице: [SHERE-2_from_appro_to_mass](https://github.com/Vetselet/SHERE-2_from_appro_to_mass)

Средние массы традиционным методом оцениваются в программе [Average_mass_with_optimization_q1q2](https://github.com/Vetselet/SHERE-2_from_appro_to_mass/blob/main/Average_mass_with_optimization_q1q2.ipynb)

## Статья

Подробный алгоритм действий и физическое обоснование представлено в статье [Latypova2023_MUPB](https://github.com/Vetselet/Task_sphere_NN/blob/main/Latypova2023_MUPB.pdf).
