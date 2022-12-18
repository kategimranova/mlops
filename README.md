# Домашнее задание 1
**Rest API, основанное на Fast API для задачи Титаник (Бинарная классификация).**
## Описание модели

(подробное описание данных и датасета: https://www.kaggle.com/competitions/titanic/data)

Для бинарной классификации используются 2 типа моделей: *KNN* и *Logistic Regression*.

В *KNN* можно регулировать параметр *n_neighbors* (количество соседей, натуральное число), в *Logistic Regression* - *penalty* (тип регуляризации: *l1*, *l2* или *none*)

## Описание входных параметров
Признаки, которые подаются на вход модели: 

*Pclass* (Класс билета) - целое число от 1 до 3

*Sex* (пол) - 'male'/'female'

*Age* (возраст) - целое число от 1 до 101

*Fare* (транспортные расходы) - float число

*Embarked* (порт) - строковые значения из 'C', 'Q', 'S'

*Relative* (количество родственников на борту) - целое неотрицательное число

##  Запуск
```bash
pip install virtualenv
virtualenv -p path_to_python venv
source venv/bin/activate
pip install -r requirements.txt
uvicorn api:app
```
Swagger документация: http://127.0.0.1:8000/docs

