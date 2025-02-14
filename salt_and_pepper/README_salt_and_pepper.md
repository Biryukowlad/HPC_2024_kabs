# ЛР 2: Salt and pepper
## Сделал Бирюков Влад 6132-010402D

## Задание

Цель: Реализовать алгоритм для фильтрации изображения от шума "соль и перец".

Язык: Python с использованием CUDA.

Входные данные: Изображение в градациях серого с шумом "соль и перец".

Выходные данные: Изображение после фильтрации + время выполнения.

Реализация: Необходимо реализовать 2 функции для фильтрации изображения: одну на CPU и одну на GPU с применением CUDA.

Эксперименты: Провести эксперименты по фильтрации изображения, посчитать ускорение.

## Ход работы

Работа реализована в Google Collab, дабы использовать их вычислительные мощности, а не мощности своего старого умирающего ноута. [Ссылка на ЛР в коллабе](https://colab.research.google.com/drive/1baVGxY1yZRCmbkZU7klPFR_x50r7N-3n?usp=sharing). В качестве изображения было взято свое фото размеров 800 на 1065 пикселей.

1. Подключение Google Drive и загрузка изображения с шумом "соль и перец".

2. Генерация изображения с шумом с использованием функции add_noise.

3. Фильтрация изображения на центральном процессоре (CPU) с помощью функции apply_salt_and_pepper_filter_cpu.

4. Замер времени выполнения на CPU.

5. Фильтрация изображения на графическом процессоре (GPU) с помощью функции apply_salt_and_pepper_filter_gpu.

6. Замер времени выполнения на GPU.

7. Подсчет ускорения

### Параллелизация

Были распараллелены математические операции (фильтрация) для вычисления пикселей результирующего изображения. Для этого данные из входного изображения передавались на устройство (GPU), чтобы все созданные потоки могли выполнить функцию ядра (median_filter_kernel) над этими данными. После выполнения вычислений результаты возвращались обратно на хост (CPU). Каждый поток (ядро CUDA) вычислял отдельный элемент результирующего изображения.