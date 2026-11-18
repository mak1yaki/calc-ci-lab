# calc-ci-lab — учебный проект для ЛПР 12

[![GitHub Actions](https://github.com/mak1yaki/calc-ci-lab/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/mak1yaki/calc-ci-lab/actions/workflows/ci.yml)
[![Bitbucket Pipelines](https://img.shields.io/bitbucket/pipelines/yarikbig/calc-ci-lab/main?label=Bitbucket%20Pipelines&logo=bitbucket)](https://bitbucket.org/yarikbig/calc-ci-lab/pipelines)

Небольшой калькулятор на Python, на примере которого настраивается непрерывная
интеграция (CI) в **GitHub Actions**, **GitLab CI/CD** и **Bitbucket Pipelines**.

## Структура

```
.
├── .github/workflows/ci.yml   # workflow GitHub Actions
├── .gitlab-ci.yml             # pipeline GitLab CI/CD
├── bitbucket-pipelines.yml    # pipeline Bitbucket Pipelines
├── pyproject.toml             # метаданные пакета и настройки pytest
├── requirements-dev.txt       # инструменты разработки (pytest, flake8, build)
├── .flake8                    # настройки линтера
├── src/calc/                  # исходный код пакета
│   ├── operations.py          # арифметические функции
│   └── cli.py                 # консольный интерфейс `calc`
└── tests/test_operations.py   # модульные тесты
```

## Локальный запуск

```bash
python -m venv .venv
# Windows: .venv\Scripts\activate      Linux/macOS: source .venv/bin/activate
pip install -r requirements-dev.txt
flake8 src tests          # проверка кода
pytest -v                 # тесты
python -m build           # сборка: dist/*.whl и dist/*.tar.gz
pip install dist/*.whl && calc add 2 3
```

## Этапы CI

| Этап  | Что делает                                   | GitHub Actions (job) | GitLab CI (job) |
|-------|----------------------------------------------|----------------------|-----------------|
| lint  | `flake8 src tests`                           | `lint`               | `lint`          |
| test  | `pytest`, отчёт JUnit                        | `test`               | `test`          |
| build | `python -m build`, проверка установки wheel  | `build`              | `build`         |
