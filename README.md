# Ранжирование документов с использованием CatBoostRanker

## Описание задачи
Задача заключается в ранжировании документов на основе признаков внутри одной сессии, используя библиотеку CatBoost.

## Данные
Для решения задачи используется датасет `intern_task.csv`.

## Модель
В качестве модели для ранжирования документов используется `CatBoostRanker`.

Параметры модели по умолчанию:

```python
default_parameters = {
    'iterations': 4000,
    'custom_metric': ['NDCG:top=5', 'AUC:type=Ranking', 'MAP:top=5'],
    'verbose': 100,
    'random_seed': 0,
    'use_best_model':True,
}
```

## Функции потерь
Для ранжирования документов были использованы следующие функции потерь:

- `PairLogit`
- `LambdaMart`
- `RMSE`
- `QuerySoftMax`

## Результаты
Результаты обучения и предсказания для каждой модели с различными функциями потерь представлены в таблице ниже:

| Функция потерь | NDCG@5 |
|----------------|--------|
| `PairLogit`    | 0.6244 |
| `LambdaMart`   | 0.6549 |
| `RMSE`         | 0.6594 |
| `QuerySoftMax` | 0.6396 |

Также были к модели `QuerySoftMax` была применена функция весов учитывающая размер сессии 

На обученных моделях была обучена модель на метаданных(бленд)

Оценены варианты преобразования данных для улучшения метрики NDCG@5(смотреть Vk3.ipynb)
