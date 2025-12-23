<div align="center">

# 🧠 LLM Zero-Shot Psychometrics

**[🇬🇧 English](#english-version) | [🇷🇺 Русский](#russian-version)**

</div>

---

<a id="english-version"></a>

## 🇬🇧 English Version

> **Code and materials for the research paper: "Evaluating the Capabilities of Modern LLMs in Automatic Psychological Text Profiling"**

This repository contains source code, validation pipelines, and experimental results for extracting psychological characteristics (MBTI, Big Five, Gender) from text using modern Large Language Models (DeepSeek V3.2, Google Gemini 3.0 Pro, Qwen 3, Aprie 1.5) in a **Zero-Shot** setting.

### 📊 Key Results

The study revealed a strong correlation between the quality of psychometric analysis and the "reasoning" capabilities of the model (measured via MMLU benchmarks).

| Model | Type | MBTI Accuracy | (I)ntroversion / (E)xtraversion | Note |
| :--- | :--- | :--- | :--- | :--- |
| **Qwen 3 8B / Apriel 1.5 15B** | Local (4-bit) | \~6% | Random | Unsuitable for zero-shot psychometrics |
| **DeepSeek V3.2** | API (FP) | 52.5% | 85.5% | Strong Baseline |
| **Gemini 3.0 Pro** | SOTA | **74.0%** | **98.0%** | Pilot Study (N=60) |

### 🚀 How to Run (Reproducibility)

⚠️ **Important:** All experiments were optimized for and conducted in the **Kaggle Notebooks** environment. The scripts utilize specific Kaggle dataset paths.

To reproduce the results, we recommend **not running the code locally**, but importing the notebooks into Kaggle and attaching the relevant datasets.

#### Instructions:

1.  Create a new notebook on [Kaggle](https://www.kaggle.com/).
2.  Import the required `.ipynb` file from the `notebooks/` folder of this repository.
3.  **Add Datasets** (Add Input) to your notebook:
    * [MBTI Type Dataset](https://www.kaggle.com/datasets/datasnaek/mbti-type)
    * [Essays Big5](https://www.kaggle.com/datasets/marii8st/essays-big5)
    * [Personae Corpus](https://www.kaggle.com/datasets/marii8st/personae-corpus)
4.  Set the necessary API keys (for DeepSeek/Gemini) in your notebook's `Secrets` or as an environment variable `NOVITA_API_KEY`.

> **Note:** Running locally will require downloading all datasets and manually changing the file paths in the code (`/kaggle/input/...` -> `your_local_paths`).

### 📂 File Description

* `notebooks/`
    * `local_models_inference.ipynb` — Experiments with quantized models (Qwen, Llava) using `transformers` and `bitsandbytes`.
    * `deepseek_inference.ipynb` — Asynchronous pipeline for DeepSeek V3.2 via API (uses `AsyncOpenAI` and `tenacity`).
* `results/`
    * Contains raw CSV files with model predictions and final accuracy metrics.

### 🛠 Tech Stack

* **Frameworks:** PyTorch, HuggingFace Transformers, Polars.
* **Models:** Qwen 3 8B, Apriel 1.5 15B, DeepSeek V3.2, Gemini 3.0 Pro.
* **Metrics:** Scikit-learn (Accuracy, F1-Macro, Precision/Recall).

### 📜 Citation

If you use materials from this repository, please cite it as follows:

```bibtex
@misc{sabitov2025psychometrics,
  author = {Timur Sabitov},
  title = {LLM Zero-Shot Psychometrics: Evaluation of Personality Profiling Capabilities},
  year = {2025},
  publisher = {GitHub},
  journal = {GitHub repository},
  howpublished = {\url{[https://github.com/your-username/LLM-ZeroShot-Psychometrics](https://github.com/your-username/LLM-ZeroShot-Psychometrics)}}
}
```

---

<a id="russian-version"></a>

## 🇷🇺 Русская версия

> **Код и материалы к исследованию: "Оценка способностей современных LLM к автоматическому психологическому профилированию текста"**

Этот репозиторий содержит исходный код, пайплайны валидации и результаты экспериментов по извлечению психологических характеристик (MBTI, Big Five, Gender) из текста с использованием современных больших языковых моделей (DeepSeek V3.2, Google Gemini 3.0 Pro, Qwen 3, Aprie 1.5) в режиме **Zero-Shot**.

### 📊 Основные результаты

В ходе исследования была выявлена зависимость качества психометрического анализа от "reasoning" способностей модели (измеряемых через бенчмарки MMLU).

| Модель | Тип | MBTI Accuracy | (I)ntroversion / (E)xtraversion | Примечание |
| :--- | :--- | :--- | :--- | :--- |
| **Qwen 3 8B / Apriel 1.5 15B** | Local (4-bit) | \~6% | Random | Непригодны для zero-shot психометрии |
| **DeepSeek V3.2** | API (FP) | 52.5% | 85.5% | Strong Baseline |
| **Gemini 3.0 Pro** | SOTA | **74.0%** | **98.0%** | Pilot Study (N=60) |

### 🚀 Как запустить код (Reproducibility)

⚠️ **Важно:** Все эксперименты были оптимизированы и проведены в среде **Kaggle Notebooks**. Скрипты используют специфические пути к датасетам Kaggle.

Для воспроизведения результатов мы рекомендуем **не запускать код локально**, а импортировать ноутбуки в Kaggle, подключив соответствующие датасеты.

#### Инструкция по запуску:

1.  Создайте новый ноутбук на [Kaggle](https://www.kaggle.com/).
2.  Импортируйте нужный файл `.ipynb` из папки `notebooks/` этого репозитория.
3.  **Добавьте датасеты** (Add Input) в ваш ноутбук:
      * [MBTI Type Dataset](https://www.kaggle.com/datasets/datasnaek/mbti-type)
      * [Essays Big5](https://www.kaggle.com/datasets/marii8st/essays-big5)
      * [Personae Corpus](https://www.kaggle.com/datasets/marii8st/personae-corpus)
4.  Установите необходимые API ключи (для DeepSeek/Gemini) в `Secrets` вашего ноутбука или переменную окружения `NOVITA_API_KEY`.

> **Примечание:** Локальный запуск потребует скачивания всех датасетов и ручного изменения путей в коде (`/kaggle/input/...` -\> `ваши_локальные_пути`).

### 📂 Описание файлов

  * `notebooks/`
      * `local_models_inference.ipynb` — эксперименты с квантованными моделями (Qwen, Llava) через `transformers` и `bitsandbytes`.
      * `deepseek_inference.ipynb` — асинхронный пайплайн для DeepSeek V3.2 через API (использует `AsyncOpenAI` и `tenacity`).
  * `results/`
      * Содержит сырые CSV файлы с предсказаниями моделей и итоговые метрики точности.

### 🛠 Используемые технологии

  * **Frameworks:** PyTorch, HuggingFace Transformers, Polars.
  * **Models:** Qwen 3 8B, Apriel 1.5 15B, DeepSeek V3.2, Gemini 3.0 Pro.
  * **Metrics:** Scikit-learn (Accuracy, F1-Macro, Precision/Recall).

### 📜 Цитирование

Если вы используете материалы этого репозитория, пожалуйста, укажите ссылку на него:

```bibtex
@misc{sabitov2025psychometrics,
  author = {Timur Sabitov},
  title = {LLM Zero-Shot Psychometrics: Evaluation of Personality Profiling Capabilities},
  year = {2025},
  publisher = {GitHub},
  journal = {GitHub repository},
  howpublished = {\url{[https://github.com/your-username/LLM-ZeroShot-Psychometrics](https://github.com/your-username/LLM-ZeroShot-Psychometrics)}}
}
```
