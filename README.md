# Project Title

This project demonstrates a simple data processing workflow using Python with Pandas, including a non-trivial error fix, data conversion, and a GitHub Actions CI/CD pipeline for linting, execution, and deployment of results via GitHub Pages.

## Table of Contents
- [Project Overview](#project-overview)
- [Files Included](#files-included)
- [Setup and Local Execution](#setup-and-local-execution)
- [GitHub Actions CI/CD](#github-actions-cicd)
- [License](#license)

## Project Overview

The core of this project is the `execute.py` script, which processes data from `data.csv`. The original `data.xlsx` file was converted to `data.csv` for streamlined processing and version control.

A significant "non-trivial" error in `execute.py` has been identified and fixed. This error typically involved robust handling of mixed data types (e.g., non-numeric entries) in numerical columns and ensuring a consistent JSON output format suitable for consumption by other applications or frontends. Specifically, the script now:
1.  Reads data from `data.csv`.
2.  Converts the 'Value' column to a numeric type, coercing errors to `NaN` and then filling `NaN` values with `0` to prevent calculation failures.
3.  Aggregates data by 'Category', summing the 'Value'.
4.  Outputs the processed data as a well-formatted JSON array of objects to `result.json`.

The project also features a GitHub Actions workflow (`.github/workflows/ci.yml`) that automates linting with Ruff, executes `execute.py`, and publishes the generated `result.json` to GitHub Pages.

## Files Included

-   `index.html`: A simple, responsive HTML page built with Tailwind CSS. It serves as a placeholder or could be extended to display the `result.json` content.
-   `execute.py`: The Python script responsible for data processing. It reads `data.csv`, performs aggregation, and outputs `result.json`.
-   `data.csv`: The input data file, converted from the original `data.xlsx`.
-   `README.md`: This file, providing an overview and instructions.
-   `LICENSE`: The MIT License covering the project.
-   `.github/workflows/ci.yml`: The GitHub Actions workflow definition.

## Setup and Local Execution

To set up and run the script locally, ensure you have Python 3.11+ and Pandas 2.3+ installed.

1.  **Clone the repository:**
    ```bash
    git clone <your-repo-url>
    cd <your-repo-name>
    ```

2.  **Create a virtual environment and install dependencies:**
    ```bash
    python -m venv .venv
    source .venv/bin/activate  # On Windows: .venv\Scripts\activate
    pip install pandas ruff
    ```

3.  **Run the data processing script:**
    ```bash
    python execute.py > result.json
    ```
    This will generate `result.json` in your current directory with the processed data.

4.  **Linting with Ruff:**
    ```bash
    ruff check .
    ruff format . --check
    ```

## GitHub Actions CI/CD

The project includes a GitHub Actions workflow (`.github/workflows/ci.yml`) that triggers on every push to the `main` branch.

The workflow performs the following steps:
1.  **Checkout Code**: Retrieves the repository content.
2.  **Setup Python**: Configures the Python environment (specifically Python 3.11).
3.  **Install Dependencies**: Installs `pandas` and `ruff`.
4.  **Run Ruff**: Executes `ruff check` to lint the Python code and displays any issues in the CI log.
5.  **Run `execute.py`**: Executes `python execute.py` and redirects its output to `result.json`.
6.  **Upload GitHub Pages Artifact**: Uploads `result.json` as an artifact named `github-pages`.
7.  **Deploy to GitHub Pages**: Deploys the uploaded artifact to GitHub Pages, making `result.json` accessible publicly at a URL like `https://<YOUR_USERNAME>.github.io/<YOUR_REPO_NAME>/result.json`.

**Note:** The `result.json` file is *not* committed to the repository; it is generated and published solely by the CI pipeline.

## License

This project is open-source and available under the [MIT License](LICENSE).
