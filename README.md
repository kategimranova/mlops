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

## Выходные параметры предсказания
Dict-объект вида
{
  "label": 0,
  "prediction": "Not survived"
}
где label ∈ {0;1}, 
prediction ∈ {"Not survived", "Survived"}

##  Запуск
```bash
cd ./mlops
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
uvicorn api:app
```
Swagger документация: http://127.0.0.1:8000/docs

## Запросы
*Получение доступных для обучения и тестирования моделей*:
```bash
curl -X GET http://localhost:8000/available_models
```
*Обучение KNN модели с параметром n_neighbors (в данном случае 3)*
```bash
curl -X 'POST' \
  'http://127.0.0.1:8000/train/knn' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "n_neighbors": 3
}'
```

*Обучение LogReg модели с параметром penalty (в данном случае l1)*
```bash
curl -X 'POST' \
  'http://127.0.0.1:8000/train/logreg' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "penalty": "l1"
}'
```
*Предсказание KNN модели*
```bash
curl -X 'POST' \
  'http://127.0.0.1:8000/predict/knn' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "Pclass": 3,
  "Sex": "male",
  "Age": 50,
  "Fare": 1,
  "Embarked": "C",
  "Relative": 1
}'
```
*Предсказание LogReg модели*
```bash
curl -X 'POST' \
  'http://127.0.0.1:8000/predict/logreg' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "Pclass": 2,
  "Sex": "male",
  "Age": 80,
  "Fare": 2,
  "Embarked": "C",
  "Relative": 2
}'
```
*Удаление модели (model_name = "KNN" или "LogisticRegression")*
```bash
curl -X 'DELETE' \
  'http://127.0.0.1:8000/delete_model' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "model_name": "KNN"
}'
```

*Общая информация*
```bash
curl -X GET http://localhost:8000/
```




