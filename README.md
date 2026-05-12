# RAG-PDF-Chatbot

This project demonstrates a simple Retrieval-Augmented Generation (RAG) workflow for chatting with a PDF inside [rag_pdf_chatbot.ipynb](rag_pdf_chatbot.ipynb).

The notebook covers:
- PDF loading and text extraction
- metadata-aware preprocessing with `pdfplumber`
- chunking with LangChain
- embedding storage in Chroma
- local answer generation with `Qwen/Qwen2.5-1.5B-Instruct`
- question answering over retrieved PDF context

## Project Files

- [rag_pdf_chatbot.ipynb](rag_pdf_chatbot.ipynb) — main notebook
- [requirements.txt](requirements.txt) — reusable Python dependencies
- [README.md](README.md) — setup and usage guide

## Prerequisites

Before running the notebook, make sure you have:

- Python 3.10 or newer
- Git
- One of the following:
	- VS Code with the Jupyter and Python extensions, or
	- Jupyter Notebook / JupyterLab, or
	- Google Colab
- Enough disk space and memory for model downloads
- Optional but recommended: a GPU for faster inference

## Clone the Repository

```bash
git clone <your-repository-url>
cd RAG-PDF-Chatbot
```

Replace `<your-repository-url>` with your actual repository URL.

## Dependency Setup

This repository now includes [requirements.txt](requirements.txt), which is the preferred setup method.

### Create a virtual environment

#### Windows (PowerShell)

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

#### macOS / Linux

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### Install dependencies from `requirements.txt`

```bash
pip install -r requirements.txt
```

### Installed packages

The requirements file includes the main dependencies used by the notebook:

- `langchain`
- `langchain-community`
- `langchain-text-splitters`
- `chromadb`
- `pypdf`
- `tiktoken`
- `pdfplumber`
- `transformers`
- `accelerate`
- `torch`
- `sentence-transformers`

## Usage Options

You can run this project in three ways.

### Option 1: VS Code workflow

1. Clone the repository.
2. Create and activate the virtual environment.
3. Install dependencies with `pip install -r requirements.txt`.
4. Open the project folder in VS Code.
5. Open [rag_pdf_chatbot.ipynb](rag_pdf_chatbot.ipynb).
6. Select the Python kernel from your `.venv` environment.
7. Place your PDF in the project folder and rename it to `sample.pdf`.
8. Run the notebook cells from top to bottom.

#### VS Code note

The notebook contains a Colab upload cell using `google.colab`. When running in VS Code, skip that upload cell unless you modify it for local file selection.

### Option 2: Google Colab workflow

1. Upload [rag_pdf_chatbot.ipynb](rag_pdf_chatbot.ipynb) to Google Colab, or open it from your GitHub repository.
2. Run the package installation cells.
3. Run the upload cell and choose your PDF file.
4. If needed, rename the uploaded file or update the notebook so the loader points to the correct PDF filename.
5. Run the remaining cells in order.

#### Colab note

Large model downloads may take time, and runtime memory limits can affect performance depending on the selected hardware.

### Option 3: Classic Jupyter workflow

1. Clone the repository.
2. Create and activate the virtual environment.
3. Install dependencies with `pip install -r requirements.txt`.
4. Start Jupyter:

```bash
jupyter notebook
```

5. Open [rag_pdf_chatbot.ipynb](rag_pdf_chatbot.ipynb).
6. Place your PDF in the project folder as `sample.pdf`.
7. Run the notebook in order.

## PDF Input Requirements

The notebook expects a PDF file named `sample.pdf`.

You can supply it in either of these ways:

- **VS Code / local Jupyter:** place the PDF in the project folder as `sample.pdf`
- **Google Colab:** upload the PDF using the notebook upload cell

If you want to use a different filename, update every notebook cell that references `sample.pdf`.

## Notebook Flow

Run the cells in order.

### 1. Environment setup

The opening cells install required packages. If you already installed from [requirements.txt](requirements.txt), these cells may be redundant.

### 2. Document loading and preprocessing

The notebook:
- loads the PDF
- extracts text and metadata with `pdfplumber`
- wraps pages as LangChain `Document` objects
- splits the text into chunks

### 3. Vector store creation

The notebook creates embeddings with `sentence-transformers/all-MiniLM-L6-v2` and stores them in Chroma.

### 4. Language model initialization

The notebook loads `Qwen/Qwen2.5-1.5B-Instruct` through Transformers.

The first run may be slow because model files must be downloaded.

### 5. Question answering

Edit the `query` variable in the question cells, then run the prompt and response cells.

Example questions already in the notebook:
- `When the 11 dec airplane crash happened?`
- `What method was used for PDF preprocessing?`

## Recommended Quick Start

For the cleanest local setup:

1. Clone the repository.
2. Create and activate `.venv`.
3. Run `pip install -r requirements.txt`.
4. Open [rag_pdf_chatbot.ipynb](rag_pdf_chatbot.ipynb) in VS Code.
5. Add your PDF as `sample.pdf`.
6. Skip the Colab upload cell.
7. Run the rest of the notebook in order.

## Notes

- The notebook currently mixes local and Colab-specific steps.
- The package installation cells can be kept for Colab, but are usually unnecessary after installing from [requirements.txt](requirements.txt) locally.
- `langchain-openai` was removed from the setup instructions because it is not used by the current notebook.
- If `torch.float16` causes issues on CPU-only machines, the model-loading cell may need adjustment.

## Troubleshooting

### `ModuleNotFoundError`

Make sure the virtual environment is active, then reinstall dependencies:

```bash
pip install -r requirements.txt
```

### PDF not found

Make sure the file exists in the project folder as `sample.pdf`, or update the filename inside the notebook.

### `google.colab` import error in VS Code or Jupyter

Skip the Colab upload cell when running locally.

### Slow inference

CPU inference can be slow. A GPU-backed environment will improve performance.

### Model download issues

Retry after confirming internet access and available disk space, especially for the Hugging Face model downloads.