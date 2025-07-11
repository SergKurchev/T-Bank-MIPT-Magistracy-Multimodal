# Инструкция по воспроизведению анализа мультимодальной модели с использованием TransformerLens

Эта инструкция описывает, как воспроизвести анализ мультимодальной модели "llava-hf/llava-1.5-7b-hf" с использованием подхода Logit Lens на платформе Kaggle. Анализ включает два основных этапа: выполнение вычислений на GPU с сохранением результатов и визуализацию с последующим анализом. Для этого используются два ноутбука и два датасета, размещённые на Kaggle.

## Требования

- **Платформа:** Kaggle Notebooks (рекомендуется использовать бесплатные вычислительные ресурсы Kaggle).
- **Датасеты:** Необходимо загрузить два датасета с Kaggle (подробности ниже).
- **Вычислительные ресурсы:**
  - Для первого ноутбука: GPU P100 (доступно в Kaggle).
  - Для второго ноутбука: любая машина Kaggle (CPU или GPU).

## Этапы выполнения

### 1. Подготовка и запуск первого ноутбука: `Make_Analyse.ipynb`

**Цель:** Выполнить анализ мультимодальной модели с использованием TransformerLens и сохранить результаты для последующей визуализации.

**Шаги:**

1. **Создание ноутбука на Kaggle:**
   - Создайте новый ноутбук на Kaggle или загрузите файл `Make_Analyse.ipynb`.
   - Убедитесь, что в настройках ноутбука выбран акселератор **GPU P100** (в разделе "Settings" → "Accelerator").

2. **Подключение датасета COCO:**
   - Добавьте датасет `COCO-data-100` в ваш ноутбук:
     - URL: [https://www.kaggle.com/datasets/sergeykurchev/coco-data-100](https://www.kaggle.com/datasets/sergeykurchev/coco-data-100)
     - В интерфейсе Kaggle перейдите в раздел "Data" → "Add Data" → найдите датасет по названию или URL и подключите его.
   - Этот датасет содержит 100 изображений из набора COCO (Common Objects in Context) и используется для быстрой загрузки данных в ноутбуке.

3. **Запуск ноутбука:**
   - Откройте `Make_Analyse.ipynb` и выполните все ячейки последовательно.
   - Ноутбук выполняет анализ мультимодальной модели "llava-hf/llava-1.5-7b-hf" с использованием Logit Lens, вычисляет промежуточные представления и сохраняет результаты (например, вероятности токенов, значения JSD) в файлы.
   - Убедитесь, что GPU P100 активен, так как вычисления требуют значительных ресурсов.

4. **Сохранение результатов:**
   - После выполнения ноутбука результаты сохраняются в формате, пригодном для последующей визуализации (например, CSV или pickle файлы).
   - Эти файлы автоматически сохраняются в папке `/kaggle/working/` или в указанную директорию в ноутбуке.
   - Для удобства дальнейшего использования рекомендуется загрузить эти результаты как датасет на Kaggle:
     - Создайте новый датасет на Kaggle (например, через "New Dataset" в вашем профиле).
     - Загрузите файлы результатов из `/kaggle/working/` и оп.edit
     - Опубликуйте датасет. Он будет доступен по ссылке: [https://www.kaggle.com/datasets/sergeykurchev/multimodal-analized-results](https://www.kaggle.com/datasets/sergeykurchev/multimodal-analized-results).

### 2. Подготовка и запуск второго ноутбука: `Visualise_Analyse.ipynb`

**Цель:** Визуализировать результаты анализа, выполненного в первом ноутбуке, и представить выводы в виде тепловых карт, графиков и текстового отчёта.

**Шаги:**

1. **Создание ноутбука на Kaggle:**
   - Создайте новый ноутбук на Kaggle или загрузите файл `Visualise_Analyse.ipynb`.
   - Этот ноутбук можно запускать на любой машине Kaggle (CPU или GPU), так как он не требует интенсивных вычислений.

2. **Подключение датасета с результатами:**
   - Добавьте датасет `multimodal-analized-results` в ваш ноутбук:
     - URL: [https://www.kaggle.com/datasets/sergeykurchev/multimodal-analized-results](https://www.kaggle.com/datasets/sergeykurchev/multimodal-analized-results)
     - В интерфейсе Kaggle перейдите в раздел "Data" → "Add Data" → найдите датасет по названию или URL и подключите его.
   - Этот датасет содержит сохранённые результаты анализа из `Make_Analyse.ipynb` (например, вероятности токенов и значения JSD).

3. **Запуск ноутбука:**
   - Откройте `Visualise_Analyse.ipynb` и выполните все ячейки последовательно.
   - Ноутбук содержит код для:
     - Визуализации вероятностей топ-1 токенов в виде тепловых карт.
     - Построения тепловых карт дивергенции Дженсена-Шеннона (JSD) для оценки изменений предсказаний по слоям.
     - Анализа топ-30 токенов по средним вероятностям.
     - Построения графика средней JSD по слоям.
   - Также в ноутбуке содержится текстовый отчёт с выводами, описывающий поведение модели и выявленные паттерны.

4. **Изучение результатов:**
   - Для понимания проведённого исследования внимательно изучите визуализации и текстовые выводы в `Visualise_Analyse.ipynb`.
   - Текстовый отчёт объясняет ключевые наблюдения, такие как распознавание цветов, объектов и взаимного расположения объектов на разных слоях.

## Датасеты

1. **COCO-data-100** ([ссылка](https://www.kaggle.com/datasets/sergeykurchev/coco-data-100)):
   - Содержит 100 изображений из датасета COCO с аннотациями объектов.
   - Используется в `Make_Analyse.ipynb` для анализа способности модели обрабатывать сложные сцены.

2. **Multimodal-analized-results** ([ссылка](https://www.kaggle.com/datasets/sergeykurchev/multimodal-analized-results)):
   - Содержит результаты анализа, полученные в `Make_Analyse.ipynb`.
   - Используется в `Visualise_Analyse.ipynb` для визуализации и интерпретации.
