#С СОХРАНЕНИЯ
# AMEX
Competition American Express
Задача заключается в определении дефолта по кредиту.
https://www.kaggle.com/competitions/amex-default-prediction/overview/description

# Решение
## Предобработка данных:
### Избавление от шумов 
%nbsp;%nbsp;%nbsp;%nbsp;Ноутбуки amex-data-int-types-train и amex-data-int-types-test предназначены для избавления от шумов.
  
### Пропуски в данных и линейнозависимые признаки
%nbsp;%nbsp;%nbsp;%nbsp;Ноутбуки fill-missing-train.ipynb и fill-missing-test.ipynb выполняют оставшуюся часть обработки. 

%nbsp;%nbsp;%nbsp;%nbsp;Первый этап заполнения пропусков начинается с помощью линейной интерполяции для вещественных признаков по записям о пользователе и отсев признаков, чьи пропуски выше 80%. удаляются из пространства. В дальнейшем оставшиеся пропуски у признаков с 90% заполненностью заменяются с помощью среднего значения для вещественных и наиболее частым для категориальных, признаки у которых заполненность меньше заполняются обученными моделями CatBoostRegressor и CatBoostClassifier обученных на заполненных признаках.

%nbsp;%nbsp;%nbsp;%nbsp;Проблема линейнозависимых признаков решается с помощью моделей линейной и логистической регрессии. Признаки, которые могут быть предсказаны ими на основе других, удаляются.
### Категориальные признаки
%nbsp;%nbsp;%nbsp;%nbsp;Информация о категориальных признаках закодирована с помощью target encoding.

# Обучение моделей
%nbsp;%nbsp;%nbsp;%nbsp;Ноутбуки create_models.ipynb и predict-test.ipynb для создания моделей и предсказания. 
Итоговое решение основано на стекинге, есть три пула моделей. Первый пул состоит из моделей логистической регрессии, которе предсказывают на основе временных рядых, состоящих из одного признака за несколько месяцев. Kоличество этих моделей равно количеству признаков. Второй пул состоит из CatBoostClassifier, которые предсказывают результат на основе одной записи пользователя. Количество этих моделей 13, как количество записей о пользователях. Модель, принимающая результаты двух пулов, CatBoostClassifier.

# Итог
Результат составил 0.75146.
