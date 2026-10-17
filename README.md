# AI Security Monitor

**An educational ML dashboard for network anomaly detection and HTTP attack-pattern classification.**

The web interface is built with Streamlit and has five sections:

- **Overview** — key counters, event charts, filters, and event log.
- **Network traffic** — upload a network-flow CSV and analyse it with Isolation Forest and Random Forest.
- **HTTP / NLP** — test a single request or upload a CSV with a `request` column; the NLP model predicts `Normal`, `SQL Injection`, or `XSS`.
- **Model quality** — test-set metrics and confusion matrices.
- **About** — methodology and limitations.

The repository includes pre-trained demo models, synthetic example datasets, event logs, and metrics so the dashboard opens without a separate training step. All demo data are synthetic.

## Run locally

Python 3.11 or 3.12 is recommended.

```bash
python -m venv .venv
# Windows:
.venv\Scripts\activate
# macOS / Linux:
source .venv/bin/activate

pip install -r requirements.txt
streamlit run app.py
```

Then open the local URL printed in the terminal (usually `http://localhost:8501`).

## Publish as a website with Streamlit Community Cloud

1. Upload the **contents of this project folder** to a GitHub repository. The `app.py` and `requirements.txt` files must be in the repository root.
2. Open [share.streamlit.io](https://share.streamlit.io/) and sign in with GitHub.
3. Select **Create app**, choose the repository and branch, and set **Main file path** to `app.py`.
4. Click **Deploy**. The first launch may take a few minutes while dependencies install.

Do not upload API keys, passwords, private logs, or sensitive traffic data. Use synthetic or approved test data only.

## Important limitations

- This is an educational prototype, not a production IDS/WAF. It does not block traffic or connect to a live network feed.
- The included data are synthetic. The scores demonstrate the workflow and must not be presented as proof of real-world performance.
- Each result is a **model prediction (unconfirmed)**. Review alerts manually.
- Avoid uploading sensitive logs to a publicly hosted deployment. For private use, run the app locally or deploy it behind appropriate access controls.

## Project structure

```text
app.py                 Streamlit web dashboard
config.py              Shared paths, columns, and safety limits
train_all.py           Train models and create evaluation outputs
src/network/           Network cleaning and ML models
src/nlp/               HTTP normalization and NLP models
src/common/            Event schema, CSV validation, metrics
models/                Included demo model files
outputs/               Demo events, metrics, and confusion matrices
data/                  Synthetic demo datasets
requirements.txt       Python dependencies
```
