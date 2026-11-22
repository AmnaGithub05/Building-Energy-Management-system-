# Building Energy Management System

## AI Data Engineering Project

This project analyzes building electricity data using Google Colab, PySpark, machine-learning
benchmarking, and Tableau. The workflow collects and verifies the source data, processes and
validates it, produces analytical features, benchmarks the pipeline, and prepares Tableau-ready
energy datasets.

## Project Structure

The notebooks and outputs should be organized in Google Drive using the following structure:

```text
CENG400_Energy_Project/
├── Part 1 results and related files/
│   ├── raw/
│   │   ├── electricity.csv
│   │   └── metadata.csv
│   └── logs/
│       └── ingestion_log.csv
├── Part 2 results and related files/
│   ├── curated/
│   ├── quality/
│   ├── analytics/
│   └── features/
├── Part 3 results and related files/
│   ├── benchmarks/
│   ├── tableau_files/
│   │   ├── monthly_energy/
│   │   ├── building_energy/
│   │   ├── hourly_energy/
│   │   ├── weekday_weekend_energy/
│   │   ├── energy_intensity/
│   │   └── anomaly_summary/
│   └── person3_machine_learning_results.csv
├── Part 1 & Part 2.ipynb
└── Part 3.ipynb
```

## Data Pipeline

### Part 1: Data Collection and Storage

Part 1 downloads the Building Data Genome Project 2 files:

- `electricity.csv`
- `metadata.csv`

The notebook verifies that the files are readable and non-empty, records their sizes and column
counts, and creates `ingestion_log.csv` with a source URL, UTC ingestion time, file size, SHA-256
checksum, verification status, and local file path.

### Part 2: PySpark Processing and Analytics

Part 2 reads the raw data and produces curated, quality, analytics, and feature datasets. These
folders are the hand-off for the Part 3 notebook:

- `curated/` — cleaned and standardized data
- `quality/` — validation and data-quality outputs
- `analytics/` — analysis-ready datasets
- `features/` — variables used by the analytical and machine-learning stages

### Part 3: Benchmarking and Tableau Exports

Part 3 reads the Part 1 and Part 2 outputs, runs the Spark benchmarks, produces machine-learning
results, and exports Tableau-ready CSV files.

## Run the Project in Google Colab

1. Upload or open the project folder in Google Drive:

   ```text
   My Drive/CENG400_Energy_Project
   ```

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

5. Run `Part 1 & Part 2.ipynb` from the first cell to the last cell.
6. Confirm that both raw files and the ingestion log exist in the Part 1 results folder.
7. Confirm that the Part 2 `curated`, `quality`, `analytics`, and `features` folders contain outputs.
8. Update and run `Part 3.ipynb` using the shared Drive layout:

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

   Set the Person 2 output variable to the Part 2 folder:

   ```python
   OUT = str(PART2)
   ```

   Then use `OUT / 'analytics'` and `OUT / 'features'` consistently for data reads.

9. Run `Part 3.ipynb` in order after the raw data and Part 2 outputs are available.

## Before Running Part 3

Check that these required inputs exist:

```text
Part 1 results and related files/raw/electricity.csv
Part 1 results and related files/raw/metadata.csv
Part 2 results and related files/analytics/
Part 2 results and related files/features/
```

Search the Part 3 notebook for old path strings such as `person2_outputs`,
`person3_benchmarks`, `tableau_files`, and root-level `/raw/` references. They should point to
the `Part 1`, `Part 2`, and `Part 3` folders shown above.

## Tableau Workbook Setup

The notebook exports the Tableau source files to:

```text
Part 3 results and related files/tableau_files/
```

Open Tableau Desktop, create a workbook, and connect to the appropriate CSV export from Google
Drive or download the export to your computer.

Recommended workflow:

1. Open Tableau Desktop.
2. Select **Text file** and connect to the exported CSV file.
3. Review column names and data types.
4. Drag the dimensions and measures into the worksheet.
5. Build the dashboard and save the workbook.
6. Save the workbook as a `.twbx` file. A packaged workbook includes the workbook and supporting
   data, while a `.twb` workbook stores the workbook separately and may require external data.

## Upload the Tableau Workbook to GitHub

1. Open the project repository on GitHub.
2. Select **Add file** > **Upload files**.
3. Drag or browse to the Tableau `.twbx` file.
4. Add a short commit message, such as `Add Tableau packaged workbook`.
5. Select **Commit changes**.

Recommended repository location:

```text
tableau/
└── building-energy-dashboard.twbx
```

For a workbook that must be viewable online, publish it to Tableau Public:

1. In Tableau Desktop, select **File** > **Save to Tableau Public As**.
2. Sign in to Tableau Public.
3. Enter a project name and publish.
4. Copy the published dashboard URL.
5. Add the Tableau Public link to this README or to the project presentation.

## Google Cloud Storage

Part 1 demonstrates local downloading and verification and copying the data to Google Drive.
The notebooks do not replace a separate Google Cloud Storage upload step. If GCS is required,
upload the source files and record the bucket name, object paths, and upload screenshots in the
project documentation.

## Expected Outputs

- Raw source data and metadata
- Ingestion checksum and verification log
- Curated, quality, analytics, and feature datasets
- Spark benchmarking results
- Machine-learning results
- Tableau-ready CSV exports
- A packaged Tableau workbook (`.twbx`)
