# Инструкция по воспроизведению результатов

## 1. Клонирование репозитория

```bash
git clone https://github.com/sidagor/educational_practice.git
cd educational_practice
```

## 2. Установка зависимостей

```bash
pip install -r requirements.txt
``` 

Если через conda:

```bash
conda create -n chemai python=3.10
conda activate chemai
pip install -r requirements.txt
```

## 3. Структура данных

Обработанные данные находятся в `data/processed/`. 

### Для воспроизведения полного пайплайна с нуля:

1. Запустить `analysis/data_analysis.ipynb` — выполнит EDA и сгенерирует обработанные датасеты
2. Данные сохранятся в `data/processed/`
3. Запустить `final_model/data_analysis_boosts_datamain_3targ_OPTUNA_FINAL_FOR_GITHUB_CORRNAMES.ipynb` 

## 4. Запуск и проверка любых моделей

Все ноутбуки самодостаточны и не зависят друг от друга. Порядок не важен.

jupyter notebook

Открыть нужный ноутбук из папки `models/` или `final_model/`. Каждый ноутбук:
- Загружает данные из `data/processed/`
- Обучает модель с 5-фолдовой кросс-валидацией
- Выводит RMSE и строит графики
- Сохраняет submissions в формате `index, IC50, CC50, SI`

### Описание ноутбуков

| Ноутбук | Датасет | Таргеты | Модели |
|---------|---------|---------|--------|
| `data_analysis_boosts_datamain_2targ` | final | 2 (SI по формуле) | RF, CB, LGB, XGB |
| `data_analysis_boosts_datamain_3targ_OPTUNA` | final | 3 | RF, CB, LGB, XGB, Optuna для CB и LGB |
| `data_analysis_boosts_dataEF_2targ` | engineered | 2 (SI по формуле) | RF, CB, LGB, XGB |
| `data_analysis_boosts_dataEF_3targ_OPTUNA` | engineered | 3 | RF, CB, LGB, XGB, Optuna для CB и LGB |
| `ensembles_4combinations_2datasets_3targets` | оба | 3 | XGB + CB, LGB + CB, XGB + LGB, XGB + CB + LGB|

### Лучшая модель

`final_model/data_analysis_boosts_datamain_3targ_OPTUNA_FINAL_FOR_GITHUB_CORRNAMES.ipynb` — LightGBM + Optuna, датасет final, 3 таргета.

## 5. Окружение

- Python 3.10 +
- Основные библиотеки:
  - catboost
  - lightgbm
  - xgboost
  - shap
  - optuna
  - scikit-learn
  - pandas, numpy, matplotlib, seaborn
- Полный список: `requirements.txt`