## UK Sanctions Case Study

Aim: Prepare sanctions data for comparing against a banks customer records.

## Execution

### Dependencies
- Data Used (Access through website): https://www.gov.uk/government/publications/the-uk-sanctions-list
- Python  3.8+
- Jupyter Notebook / Anaconda
- Libraries: numpy, pandas, sys, warnings, os

### How to run
- Clone/download this repository.
- Create "data" folder in root directory and upload latest UK_Sanctions.csv inside.
- Open the Jupyter Notebook.
- Change '...' within directories to own pathway.
- Click **Kernel > Restart & Run All**.
- Pipeline will automatically create an `output_data/` folder containing the relational CSV files and main dataset.

### Data Quality Insights (EDA Findings)
During exploratory data analysis, several data quality issues were identified:

* **Naming:** The raw `Name 6` column does not represent a 6th given name; it represents the Surname (or full Entity name). Reconstructs the `Full Name` combining `Name 1-5` and `Name 6`.
* **Excel Formatting:** Identifier columns (e.g., Passport Numbers) contained leading apostrophes (`'0601...`) due to Excel string-forcing. These were successfully stripped without removing valid alphabetic characters present in international IDs.
* **DOB Formats:** Date of Birth entries range from full dates to partial years to free-text (`circa 1965`). Forcing datetime would cause severe data loss (`NaT`). Therefore, DOBs were standardized as uppercase strings to preserve partial intelligence for year-only matching.
* **Gender Normalization:** Gender entries contained various casing. Standardized to uniform 'Male' and 'Female' labels

### Output
Main Dataset & Three relational data bases:
- **`entities_master.csv`**: The master table containing exactly one row per Unique ID. Holds core identity and operational data (Primary Name, DOB, Identifiers).
- **`aliases.csv`**: A one-to-many table mapping Unique IDs to all known alternate names, alongside their standardized alias strength/quality. Optimized for fuzzy matching.
- **`addresses.csv`**: A one-to-many table mapping Unique IDs to all known addresses, countries, and contact details (email/phone) for geographic risk flagging.


### Comments
Some of the column names in the government provided documentation on this data set did not match the given names within the actual CSV file.
Main dataset output is not uploaded; file is too large.
