# VHoang Project

Data analysis workspace for exploring delivery routes inside a single Jupyter notebook. The project keeps its Python virtual environment in `env/` and expects CSV inputs under `project/data/`.

## Repository layout

- `project/code.ipynb` – main analysis notebook.
- `project/data/` – place input CSV files such as `deliveries.csv` and `routes.csv` (ignored by Git by default).
- `env/` – local Python virtual environment (also ignored by Git).

## Getting started

1. **Create a virtual environment**
   ```bash
   python3 -m venv env
   source env/bin/activate
   ```
2. **Install dependencies** – install the libraries you need with pip, for example:
   ```bash
   pip install -r requirements.txt  # if you export one
   ```
   If you do not have a requirements file yet, install the packages you use manually (e.g. `pip install pandas jupyter python-dotenv`), then record them with `pip freeze > requirements.txt` so they can be reproduced later.

3. **Start Jupyter**
   ```bash
   jupyter notebook project/code.ipynb
   ```

## Managing data files

`project/data/` is ignored by Git to avoid committing large datasets. Add or update the CSV inputs locally. If any sample data should live in the repository, remove the folder from `.gitignore` and add lightweight examples instead.

## Environment variables

If the notebook expects secrets or configuration values, create a `.env` file next to the notebook (or at the repo root) and populate it with the required keys. The code already calls `load_dotenv`, so variables defined there will be available inside the notebook once loaded.

Example `.env` file:

```env
# API keys / secrets
GOOGLE_APPLICATION_CREDENTIALS=credentials/service-account.json
GOOGLE_MAPS_KEY=your-google-maps-api-key

# Notebook configuration
DATA_DIR=project/data
```

Keep this file out of version control (the filename stays ignored by default).

## Google Cloud sign-in

Before running notebooks or scripts that call Google Cloud APIs, make sure you are authenticated in the Google Cloud CLI:

```bash
gcloud auth login
gcloud config set project <your-gcp-project-id>
```

If you have not configured the CLI yet, run `gcloud init` first.
