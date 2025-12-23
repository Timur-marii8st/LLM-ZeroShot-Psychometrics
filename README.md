Вот обновленный `README.md`, отражающий изменения в статье (переход от Pilot Study к полноценному N=800, смена модели на Gemini 3.0 Flash и уточнение метрик).

<div align="center">

# 🧠 LLM Zero-Shot Psychometrics

**[🇬🇧 English](#english-version) | [🇷🇺 Русский](#russian-version)**

</div>

---

<a id="english-version"></a>

## 🇬🇧 English Version

> **Code and materials for the research paper: "Evaluating the Capabilities of Modern LLMs for Automatic Text-Based Psychological Profiling in a Zero-Shot Setting"**

This repository contains source code, validation pipelines, and experimental results for extracting psychological characteristics (MBTI, Big Five, Gender) from text using modern Large Language Models (DeepSeek V3.2, Google Gemini 3.0 Flash, Qwen 3, Apriel 1.5) in a **Zero-Shot** setting.

### 📊 Key Results

The study revealed a strong correlation between the quality of psychometric analysis and the architectural complexity of the model. We observed a massive **scaling effect**, where SOTA models achieve expert-level accuracy on standard datasets but struggle with domain transfer.

**Comparative Performance on MBTI Dataset (N=800):**

| Model | Type | MBTI Exact Match | (I)ntroversion / (E)xtraversion | Note |
| :--- | :--- | :--- | :--- | :--- |
| **Qwen 3 8B / Apriel 1.5 15B** | Local (4-bit) | \~6% | Random | Unsuitable for zero-shot psychometrics |
| **DeepSeek V3.2** | API (FP) | 52.50% | 85.50% | Strong Baseline |
| **Gemini 3.0 Flash** | Efficient SOTA | **71.88%** | **91.38%** | **Full Study (N=800)** |

> **Key Insight:** The Gemini 3.0 Flash model achieved **94.00%** accuracy on the *Intuition (N) vs. Sensing (S)* axis, suggesting that abstract vs. concrete speech patterns are the most distinguishable features for LLMs. However, the model showed significant performance drops on the **Personae Corpus** (Gender/MBTI), highlighting the **Domain Shift** problem.

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
4.  Set the necessary API keys (for DeepSeek/Gemini) in your notebook's `Secrets`.

> **Note:** Running locally will require downloading all datasets and manually changing the file paths in the code (`/kaggle/input/...` -> `your_local_paths`).

### 📂 File Description

* `notebooks/`
    * `local_models_inference.ipynb` — Experiments with quantized models (Qwen, Llava) using `transformers` and `bitsandbytes`.
    * `deepseek_inference.ipynb` — Pipeline for DeepSeek V3.2 via API.
    * `gemini_inference.ipynb` — Pipeline for Google Gemini 3.0 Flash via Vertex AI/Google AI Studio.
* `results/`
    * Contains raw CSV files with model predictions and final accuracy metrics for all datasets.

### 🛠 Tech Stack

* **Frameworks:** PyTorch, HuggingFace Transformers, Polars.
* **Models:** Qwen 3 8B, Apriel 1.5 15B, DeepSeek V3.2, Gemini 3.0 Flash.
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
  howpublished = {\url{https://github.com/Timur-marii8st/LLM-ZeroShot-Psychometrics}}
}
```

---

<a id="russian-version"></a>

## 🇷🇺 Русская версия

> **Код и материалы к исследованию: "Оценка способностей современных LLM к автоматическому психологическому профилированию текста в режиме Zero-Shot"**

Этот репозиторий содержит исходный код, пайплайны валидации и результаты экспериментов по извлечению психологических характеристик (MBTI, Big Five, Gender) из текста с использованием современных больших языковых моделей (DeepSeek V3.2, Google Gemini 3.0 Flash, Qwen 3, Apriel 1.5) без предварительного обучения (Zero-Shot).

### 📊 Основные результаты

В ходе исследования была подтверждена гипотеза линейной репрезентации: качество психометрического анализа масштабируется вместе со сложностью модели. SOTA-модели достигают точности, сравнимой с надежностью психологических тестов, но страдают от смены домена текста (Domain Shift).

**Сравнительная эффективность на датасете MBTI (N=800):**

| Модель | Тип | MBTI Exact Match | (I)ntroversion / (E)xtraversion | Примечание |
| :--- | :--- | :--- | :--- | :--- |
| **Qwen 3 8B / Apriel 1.5 15B** | Local (4-bit) | \~6% | Random | Непригодны для zero-shot психометрии |
| **DeepSeek V3.2** | API (FP) | 52.50% | 85.50% | Strong Baseline |
| **Gemini 3.0 Flash** | Efficient SOTA | **71.88%** | **91.38%** | **Full Study (N=800)** |

> **Инсайт:** Модель Gemini 3.0 Flash показала рекордную точность **94.00%** на оси *Интуиция (N) — Сенсорика (S)*. Это говорит о том, что различие между абстрактным и конкретным стилями речи является наиболее "читаемым" сигналом для LLM. Однако на датасете **Personae Corpus** результаты значительно упали, что указывает на проблему переноса знаний между доменами.

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
4.  Установите необходимые API ключи (для DeepSeek/Gemini) в `Secrets` вашего ноутбука.

> **Примечание:** Локальный запуск потребует скачивания всех датасетов и ручного изменения путей в коде (`/kaggle/input/...` -\> `ваши_локальные_пути`).

### 📂 Описание файлов

  * `notebooks/`
      * `local_models_inference.ipynb` — эксперименты с квантованными моделями (Qwen, Llava) через `transformers` и `bitsandbytes`.
      * `deepseek_inference.ipynb` — пайплайн для DeepSeek V3.2 через API.
      * `gemini_inference.ipynb` — пайплайн для Google Gemini 3.0 Flash через Vertex AI/Google AI Studio.
  * `results/`
      * Содержит сырые CSV файлы с предсказаниями моделей и итоговые метрики точности для всех датасетов.

### 🛠 Используемые технологии

  * **Frameworks:** PyTorch, HuggingFace Transformers, Polars.
  * **Models:** Qwen 3 8B, Apriel 1.5 15B, DeepSeek V3.2, Gemini 3.0 Flash.
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
  howpublished = {\url{https://github.com/Timur-marii8st/LLM-ZeroShot-Psychometrics}}
}
```