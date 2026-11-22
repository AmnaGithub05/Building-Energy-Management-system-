# Building Energy Management System

## AI Data Engineering Project

This project applies Google Colab, PySpark, machine learning, and Tableau to building electricity
data. It covers data ingestion and verification, data-quality processing, analytical datasets,
performance benchmarking, machine-learning outputs, and a Tableau dashboard.

## Project Files

The repository contains the project notebooks and Tableau workbook:

```text
Building-Energy-Management-system/
├── README.md
├── Part 1 & Part 2.ipynb
├── Part 3.ipynb
├── Building Energy Management Dashboard.twbx
└── Part 3 results and related files-20261122T143434Z-1-001.zip
```

The large source datasets and the complete shared Google Drive project are available in
[this Google Drive folder](https://drive.google.com/drive/folders/19MeKkSafIme-3gCI4TjPtCqG9urWcmM3?usp=drive_link).
If a file is not available on GitHub, use the Drive folder to access it.

Drive access may require permission from the folder owner.

## Google Drive Structure

The shared Drive folder contains:

```text
CENG400_Energy_Project/
├── Part 1 results and related files/
├── Part 2 results and related files/
├── Part 3 results and related files/
├── Part 1 & Part 2.ipynb
└── Part 3.ipynb
```

The uploaded Part 3 zip contains the exported analytics and benchmark outputs, including:

- `benchmark_setup.json`
- `input_dataset_dimensions.csv`
- `data_quality_validation.csv`
- `end_to_end_test_results.csv`
- `single_node_all_workloads.csv`
- `single_node_small_medium.csv`
- `person3_machine_learning_results.csv`
- `hourly_energy/hourly.csv`
- `monthly_energy/part-00000-*.csv`
- `building_energy/buildingenergy.csv`
- `weekday_weekend_energy/WEEKDAY_WEEKEND.csv`
- `energy_intensity/energyintensity.csv`
- `anomaly_summary/anomalysum.csv`
- Runtime and throughput figures

## Data Pipeline

### Part 1: Data Collection and Storage

Part 1 obtains the Building Data Genome Project 2 source files:

- `electricity.csv`
- `metadata.csv`

It verifies the files, records their file size and column count, and creates an ingestion log with
the source URL, UTC ingestion time, verification status, local path, and SHA-256 checksum.

### Part 2: PySpark Processing and Analytics

Part 2 reads the raw source data and creates:

- Curated datasets
- Data-quality outputs
- Analytics datasets
- Feature datasets

These outputs provide the inputs used in Part 3.

### Part 3: Benchmarking, Machine Learning, and Tableau Exports

Part 3:

- Reads the Part 1 and Part 2 outputs
- Runs small, medium, and end-to-end Spark benchmarks
- Produces machine-learning results
- Generates hourly, monthly, building, weekday/weekend, intensity, and anomaly exports
- Produces data for the Tableau dashboard

## Run the Notebooks in Google Colab

1. Open the [shared Google Drive folder](https://drive.google.com/drive/folders/19MeKkSafIme-3gCI4TjPtCqG9urWcmM3?usp=drive_link).
2. Open `Part 1 & Part 2.ipynb` in Google Colab.
3. Mount Google Drive:

   ```python
   from google.colab import drive
   drive.mount('/content/drive')
   ```

4. Set the project root:

   ```python
   from pathlib import Path

   PROJECT = Path('/content/drive/MyDrive/CENG400_Energy_Project')
   ```

5. Run `Part 1 & Part 2.ipynb` from the first cell through the final Part 2 cell.
6. Confirm that the raw data and Part 1 log exist.
7. Confirm that the Part 2 folders contain their curated, quality, analytics, and feature outputs.
8. Open `Part 3.ipynb` and update its path definitions to use:

   ```python
   from pathlib import Path

   PROJECT = Path('/content/drive/MyDrive/CENG400_Energy_Project')
   PART1 = PROJECT / 'Part 1 results and related files'
   PART2 = PROJECT / 'Part 2 results and related files'
   PART3 = PROJECT / 'Part 3 results and related files'

   raw_electricity = PART1 / 'raw' / 'electricity.csv'
   raw_metadata = PART1 / 'raw' / 'metadata.csv'
   BENCHMARK_DIR = PART3 / 'benchmarks'
   TABLEAU_DIR = PART3 / 'tableau_files'

   BENCHMARK_DIR.mkdir(parents=True, exist_ok=True)
   TABLEAU_DIR.mkdir(parents=True, exist_ok=True)
   ```

9. Run `Part 3.ipynb` only after the Part 1 and Part 2 outputs are available.

## Tableau Dashboard

The Tableau packaged workbook is:

```text
Building Energy Management Dashboard.twbx
```

Download the `.twbx` file from GitHub or from the shared Drive folder, then open it in Tableau
Desktop or Tableau Public. Tableau packaged workbooks include the workbook and supporting data.

To open or recreate the dashboard:

1. Download the `.twbx` file.
2. Open it in Tableau Desktop.
3. If recreating the connection manually, use the CSV files in the Part 3 results folder.
4. Review the uploaded machine-learning, benchmark, and energy-intensity outputs.
5. Save the final dashboard as a `.twbx` file.

## Accessing Missing Files

If a notebook output, CSV dataset, or supporting file is not visible on GitHub:

1. Open the [shared Google Drive folder](https://drive.google.com/drive/folders/19MeKkSafIme-3gCI4TjPtCqG9urWcmM3?usp=drive_link).
2. Check the relevant `Part 1`, `Part 2`, or `Part 3` results folder.
3. Request folder access if Google Drive displays a permission message.
4. Download the required file and keep the original filename and folder structure.

The 174 MB source `electricity.csv` should remain in Google Drive or Google Cloud Storage instead
of being uploaded directly to GitHub.

## GitHub Workflow

The repository is intended for the notebooks, source code, dashboard workbook, and compact result
files. Large raw datasets and intermediate Spark outputs are retained in Google Drive.

## Expected Outputs

- Raw source data and metadata
- Ingestion verification log
- Curated, quality, analytics, and feature datasets
- Spark benchmark results
- Machine-learning results
- Tableau-ready CSV exports
- Tableau packaged workbook
