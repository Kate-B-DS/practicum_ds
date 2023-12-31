## Данные

Признаки:
 - RowNumber — индекс строки в данных
 - CustomerId — уникальный идентификатор клиента
 - Surname — фамилия
 - CreditScore — кредитный рейтинг
 - Geography — страна проживания
 - Gender — пол
 - Age — возраст
 - Tenure — сколько лет человек является клиентом банка
 - Balance — баланс на счёте
 - NumOfProducts — количество продуктов банка, используемых клиентом
 - HasCrCard — наличие кредитной карты
 - IsActiveMember — активность клиента
 - EstimatedSalary — предполагаемая зарплата
 - 
Целевой признак:
 - Exited — факт ухода клиента

## Задача

Из «Бета-Банка» стали уходить клиенты. Каждый месяц. Немного, но заметно. Банковские маркетологи посчитали: сохранять текущих клиентов дешевле, чем привлекать новых.

Нужно спрогнозировать, уйдёт клиент из банка в ближайшее время или нет. 
Т.е. в данном проекте целевой признак-категориальный, перед нами задача бинарной классификации. Модель будет обучаться с "учителем".

Нам предоставлены исторические данные о поведении клиентов и расторжении договоров с банком.

Нужно построить модель с предельно большим значением F1-меры. Данную метрику нужно довести до 0.59. 
А также проверить F1-меру на тестовой выборке.

И дополнительно измерить AUC-ROC, сравнивая её значение с F1-мерой.

## Результаты

В ходе поиска лучшей модели для предсказания оттока клиентов из банка, была проведена следующая работа:

 - Датасет исследован на пропуски и дубликаты, пропуски устранены.
 - Удалены лишние для работы признаки RowNumber, CustomerId, Surname.
 - Исследован баланс классов в целевом признаке. Выявлен дисбаланс.
 - Выборка разбита на тренировочную, валидационную и тестовую в соотношении 3:1:1.
 - Задача исследована на выборке без учета дисбаланса и показала результаты близкие к результатам случайной модели.
 - Для устранения дисбаланса применены три методики: upsampling, downsampling, и применение гиперпараметра class_weight='balanced' внутри моделей.
 - В результате лучшим вариантом оказалось использование гиперпараметра class_weight='balanced' внутри моделей.
 - Однако метрика лучшей модели Случайного леса F1-score на тестовой выборке не достигла требуемой 0,59, поэтому поторебовался поиск лучших гиперпараметров с помощью GridSearchCV:
 - Лучшие гиперпараметры: {'class_weight': 'balanced', 'criterion': 'gini', 'max_depth': 8, 'n_estimators': 19}
 - Лучший f1-score = 0.61.
 - На тестовой выборке лучшая модель Случайного леса с подобранными "по сетке" гиперпараметрами показала следующие результаты:
    - F1_score = 0.6
    - ROC_auc = 0.85
 - Дополнительно построен график ROC-AUC, и показана важность признаков: самыми важными оказался возраст клиентов и кол-во продуктов, которые клиент приобрел ранее.

## Используемые библиотеки

- *pandas*
- *numpy*
- *scikit-learn*
- *matplotlib*


