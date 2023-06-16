# Task_sphere_NN
Classification/regression issue. Search for an alternative criterion for better separation of events by primary masses

Существуют исходные данные, полученные в результате моделирования событий широких атмосферных ливней. Поскольку их объем очень велик, Github не позволяет их внести. Вскоре они будут перенесены на Google Disk.

Исходные данные преобразуются в данные, которые будут поданы на вход нейронной сети, с помощью программы [Data_sphere_10-20_to_maps.ipynb](https://github.com/Vetselet/Task_sphere_NN/blob/main/Data_sphere_10-20_to_maps.ipynb)  

Полученные преобразованные данные хранятся в папках на Google Disk

[https://drive.google.com/data_to_NN_q1_900_10PeV_10-20](https://drive.google.com/drive/folders/1Avlm3dYyPC1Rwx6POeY_K8bTmsunCST3?usp=sharing)

[https://drive.google.com/data_to_NN_q2_900_10PeV_10-20](https://drive.google.com/drive/folders/14b8fn_2X3asCzp-rxP-lPI0b7qsscyz8?usp=sharing)

Предобработанные данные подаются на вход нейронной сети в программе [Baseline_NN_sphere_mass_10_20_from_GC.ipynb](https://github.com/Vetselet/Task_sphere_NN/blob/main/Baseline_NN_sphere_mass_10_20_from_GC.ipynb)

В результате получается решение задачи регрессии.

Полученные данные о регрессии для большого числа событий представляют собой альтернативный критерий, который необходим для восстановления массы первичной частицы, образовавшей широкий атмосферный ливень.

