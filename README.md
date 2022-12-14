# 9_gold_recovery
# Описание проекта
***!!!РАЗМЕР ФАЙЛОВ С ДАННЫМИ ПРЕВЫСИЛ 25 МБ, ПОЭТОМУ КАЖДЫЙ ФАЙЛ БЫЛ ОТДЕЛЬНО АРХИВИРОВАН!!!***
* Компания: «Цифра»
* Отрасль: золотодобывающая


**Описание данных**
* Данные содержат **параметры добычи и очистки**
* Наименование признаков должно быть такое: **[этап].[тип_параметра].[название_параметра]** (например, **rougher.input.feed_ag**)
* Возможные значения для блока **[этап]**:
    - rougher — флотация
    - primary_cleaner — первичная очистка
    - secondary_cleaner — вторичная очистка
    - final — финальные характеристики
* Возможные значения для блока **[тип_параметра]**:
    - input — параметры сырья
    - output — параметры продукта
    - state — параметры, характеризующие текущее состояние этапа
    - calculation — расчётные характеристики


**Цель исследовани**: подготовить прототип модели машинного обучения для «Цифры». Модель должна предсказать коэффициент восстановления золота из золотосодержащей руды. Модель поможет оптимизировать производство, чтобы не запускать предприятие с убыточными характеристиками.


**Задачи исследования**:
* Выгрузить данные
* Изучить данные:
    - Проверить, что эффективность обогащения рассчитана правильно:
        - Вычислить её на обучающей выборке для признака `rougher.output.recovery`.
        - Найти MAE между вашими расчётами и значением признака на обучающей выборке.
        - Сделать краткий вывод.
* Выявить возможные проблемы в данных:
    - Наличие пропусков
    - Наличие дубликатов
    - Наличие выбросов
    - Прочие
* Осуществить предобработку данных (устранить выявленные проблемы, выявленные при выполнении предыдущей задачи)
* Проанализировать данные:
    - Посмотреть, как меняется концентрация металлов (Au, Ag, Pb) на различных этапах очистки. Сделать вывод.
    - Сравнить распределения размеров гранул сырья на обучающей и тестовой выборках (если распределения сильно отличаются друг от друга, оценка модели будет неправильной).
    - Исследуйте суммарную концентрацию всех веществ на разных стадиях: в сырье, в черновом и финальном концентратах.
    - При наличии аномальных значений в распределениях устранить их.
* Построение моделей машинного обучения:
    - Создать функцию для вычисления метрики sMAPE
    - Обучиить разные модели и оцените их качество кросс-валидацией:
        - Модель для целевого признака **`rougher.output.recovery`** по логике технологического процесса **необходимо оценивать по характеристикам, соответствующим этапу флотации**. Коэффициент восстановления золота на этапе флотации не может зависеть от последущих этапов (первичной и вторичной очисток). **Поэтому данные, характеризующие последущие этапы обработки нас не будут интересовать.**
        - Модель для целевого признака **`final.output.recovery`** по логике технологического процесса **необходимо оценивать по  характеристикам всех этапов обогащения**. **Коэффициент восстановления золота в конце технологическго процесса зависит от характеристик сырья, концентратов на всех предшедствующих этапах.**
        - Выбрать наилучшую модель.
