# 🩺 Medical Radiologist AI Agent



[![Python Version](https://img.shields.io/badge/python-3.8%2B-blue.svg)](https://www.python.org/)
[![OpenAI](https://img.shields.io/badge/Model-OpenAI%20GPT--4o--mini-green.svg)](https://openai.com/)
[![Gradio](https://img.shields.io/badge/UI-Gradio-orange.svg)](https://gradio.app/)

**Medical Radiologist AI Agent** is a multimodal, Retrieval-Augmented Generation (RAG) powered AI assistant designed to automate and enhance the workflow of medical image analysis. By combining traditional computer vision techniques with state-of-the-art Large Language Models (LLMs), this agent acts as an interactive co-pilot for radiologists, generating professional, explainable, and evidence-based diagnostic reports.

## ✨ Key Features

* **🗄️ Native `.mat` Data Ingestion:** Robustly parses raw medical data formats (MATLAB `.mat` files, supporting both v7 and v7.3 `h5py` standards), extracting 2D image matrices and physician-annotated tumor masks directly from the Figshare brain tumor dataset.
* **👁️ Unsupervised Segmentation & CV Pipeline:** Implements a highly customized, training-free computer vision pipeline (combining K-Means clustering, Canny edge detection, and morphological operations) to accurately segment lesions, calculate Dice scores, and generate visually clear BGR overlays.
* **🧠 Multimodal Semantic Observation:** Utilizes OpenAI's Vision capabilities to analyze image overlays alongside extracted mathematical features, generating structured semantic observations (JSON format).
* **📚 Retrieval-Augmented Generation (RAG):** Integrates `SentenceTransformers` and an `Annoy` vector database. The agent retrieves similar historical medical cases from a knowledge base to ground its diagnostic reasoning, significantly reducing LLM hallucinations.
* **💰 Smart Local Caching:** Built-in caching mechanism (`_semantic.json`) for API responses. It skips redundant API calls if semantic observations already exist, saving time and API costs.
* **💬 Interactive Gradio UI:** A complete, user-friendly web interface allowing doctors to select cases, chat dynamically with the AI Agent, inspect retrieved RAG cases, and download final comprehensive medical reports.

## 📊 Dataset & Evaluation

* **Original Dataset:** The raw medical imaging dataset used for this project is publicly available on Figshare: [doi:10.6084/m9.figshare.1512427](https://doi.org/10.6084/m9.figshare.1512427).
* **Testing Data (`data/`):** Due to the massive size of the original dataset, only **10 representative raw images** are uploaded to the `data/` folder in this repository. These are provided for quick testing, code reproduction, and pipeline verification.
* **Full Results (`full_dataset_results/`):** To demonstrate the model's capabilities at scale, the complete dataset's image segmentation results, generated RAG reports, and full evaluation metrics have been pre-computed and are available in the `full_dataset_results/` directory for reference.

## 🏗️ Architecture & Workflow

1.  **Raw Data Parsing (`scipy`, `h5py`):** Ingests raw `.mat` files to extract brain MRI images and ground-truth tumor masks.
2.  **Segmentation & Evaluation:** Applies an unsupervised clustering algorithm to generate predicted masks and calculates performance metrics (Dice, IoU) against ground truth.
3.  **CV Feature Extraction (`cv2`, `skimage`):** Extracts quantitative morphological features (Area, Perimeter, Circularity, etc.) and creates annotated overlay panels (saved as PNGs).
4.  **Semantic Agent (`OpenAI API`):** Analyzes the generated overlay images and outputs structured medical findings.
5.  **Knowledge Retrieval (`Annoy`):** Embeds the query and fetches the top-K most similar historical cases.
6.  **Report Generation:** An LLM synthesizes the quantitative data, semantic findings, and retrieved RAG context into a cohesive diagnostic report.
7.  **Human-in-the-Loop:** Doctors review, chat, and refine the output via the Gradio UI.

## 🚀 Getting Started

### Prerequisites

* Python 3.8+
* An active [OpenAI API Key](https://platform.openai.com/api-keys)

### Installation

**1. Clone this repository:**

```bash
git clone https://github.com/jt3645-arch/Medical-Radiologist-AI-Agent.git
cd Medical-Radiologist-AI-Agent
```

**2. Install the required dependencies:**

```bash
pip install -r requirements.txt
```

### Running the Agent

This project is optimized for Jupyter Notebook / Google Colab environments.

**Step 1:** Open `6895project_radiologist_agent.ipynb`.
**Step 2:** Set your OpenAI API Key securely when prompted in the notebook.
**Step 3:** Run all cells (`Run All`). 
**Step 4:** At the final cell, a **Gradio web interface link** will be generated. Click the public URL to start interacting with your Radiologist Agent!

## 📂 Project Structure

```text
Medical-Radiologist-AI-Agent/
├── 6895project_radiologist_agent.ipynb  # Main pipeline and UI launcher
├── requirements.txt                     # Python dependencies
├── data/                                # 10 raw sample images for testing/reproduction
├── full_dataset_results/                # Pre-computed reports, splits, and metrics
└── outputs_doc/                         # Auto-generated workspace for the test run
    ├── panels/                          # Split original & mask images
    ├── overlays/                        # Annotated BGR overlays & Semantic JSON caches
    └── final_reports/                   # Generated text reports
```

## 🛠️ Tech Stack

* **Core Logic:** Python, Pandas, Numpy
* **Computer Vision:** OpenCV (`cv2`), Pillow (`PIL`)
* **LLM & Vision:** OpenAI API (`gpt-4o` / `gpt-4o-mini`)
* **Vector DB & Embedding:** Annoy, SentenceTransformers (`all-MiniLM-L6-v2`)
* **User Interface:** Gradio

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the [issues page](https://github.com/jt3645-arch/Medical-Radiologist-AI-Agent/issues).

---
*Developed with ❤️ by [jt3645-arch](https://github.com/jt3645-arch).*
