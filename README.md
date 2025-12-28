# Resume Screening Agent

Jupyter notebook that ingests a resume PDF, extracts text with pdfplumber, and uses a Flan-T5 text2text model to compare the resume against a job description. It also performs simple keyword-based skill matching for a quick percentage score.

## Requirements
- Python 3.9+ recommended
- pip
- ~1.5 GB free disk for the `google/flan-t5-base` model download

## Setup
1) Clone the repo and open it in VS Code.
2) Pick your environment:
   - VS Code (local) — see steps below.
   - Google Colab — see steps below.

## VS Code (local) installation
1) Create/activate a virtualenv (recommended):
   ```bash
   python -m venv .venv
   .venv\Scripts\activate
   ```
2) Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3) Enable widgets in Jupyter (if needed):
   ```bash
   jupyter nbextension enable --py widgetsnbextension
   ```
4) Launch VS Code and open the notebook `resumeScreening.ipynb`.
5) Select the `.venv` kernel when prompted, then run cells in order.

## Google Colab installation
1) Upload `resumeScreening.ipynb` to Colab.
2) Run a setup cell at the top (one time per session):
   ```python
   !pip install transformers pdfplumber torch accelerate ipywidgets nltk
   ```
3) If the file upload widget is not visible, run:
   ```python
   from google.colab import output
   output.enable_custom_widget_manager()
   ```
4) Execute the notebook cells in order. Use the upload widget to provide a PDF resume.

## Usage
1) Open `resumeScreening.ipynb` and run the cells in order.
2) When prompted, upload a resume PDF via the file upload widget.
3) Adjust `job_description` in the notebook to match the role you are screening for.
4) The notebook prints:
   - Matched skills (from a simple skill bank)
   - Match percentage (10% per matched skill, capped at 100%)
   - Final decision from the LLM prompt

## Data handling
- Resume files are excluded from version control via `.gitignore` (pdf/doc/docx/rtf patterns).
- No resumes are stored on disk by the notebook; uploads stay in memory unless you add saving logic.

## Notes and troubleshooting
- If PyTorch CUDA warnings appear on CPU-only machines, they can be ignored; the pipeline runs on CPU by default.
- If `ipywidgets` UI does not appear, restart the kernel after enabling the nbextension.
- For different models, change the `pipeline` call in the notebook. Ensure the model fits your hardware.
