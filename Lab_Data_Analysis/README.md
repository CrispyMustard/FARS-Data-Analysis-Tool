FARS Data Analysis Pipeline: Truck & Curve AnalyzerA Python-based data pipeline designed to automate the analysis of NHTSA Fatality Analysis Reporting System (FARS) data. This script specifically targets the intersection of Large Truck crashes and Roadway Curvature across multiple years.

📌 Overview: This tool solves the challenge of analyzing FARS data that is split across multiple files and years. It automatically detects data folders, handles inconsistent file naming (case-sensitivity), and merges "Raw" vehicle data with "Auxiliary" data to generate safety insights.

🚀 Key FeaturesAuto-Discovery: Automatically scans your Google Drive folder structure to find year-based datasets (e.g., 2020, 2021).Case-Insensitive Loading: intelligently finds files like veh_aux.csv even if the config expects VEH_AUX.csv.Standardization: Normalizes column names (e.g., converting VALIGN to V_ALIGN) to ensure code works across different FARS eras.Robust Merging: Joins datasets using composite keys (ST_CASE + VEH_NO) to ensure data integrity.

📂 Required Folder StructureThe script is configured to look inside a specific Base Directory on Google Drive. Ensure your data is organized as follows:Plaintext/content/drive/MyDrive/Lab/Lab_Data_Analysis/  <-- Your BASE_DIR
│
├── 2021/

│   ├── vehicle.csv    # Raw Data (Contains V_ALIGN)
│   └── VEH_AUX.csv    # Aux Data (Contains A_BODY)
│
├── 2022/

│   ├── vehicle.csv
│   └── veh_aux.csv    # (Script handles lowercase names automatically)
│
└── ... (Other years)
🛠️ Setup & Usage

1. DependenciesThe script relies on pandas. If running locally or in a fresh environment, install it via:Bashpip install pandas

2. Configuration

At the top of the script, the CONFIG dictionary controls the execution.BASE_DIR: The root folder where your year subfolders are located.CODES: The specific FARS manual codes used for filtering.LARGE_TRUCK: [4] (Standard FARS code for Large Trucks)CURVES: [2, 3, 4] (Standard FARS codes for Right, Left, and Unknown curves)3. Running the ScriptRun the script in your Python environment (VS Code, Google Colab, or Jupyter).Input: It will recursively search BASE_DIR.Output: It will print a summary table to the console showing the count of truck crashes on curves per year.📊 Data Logic & Calculated FieldsThe script generates a master DataFrame (final_df) with the following added columns:Column NameTypeDescriptionYEARIntegerThe year derived from the folder name.is_large_truckBooleanTrue if A_BODY matches the configured truck codes.is_curveBooleanTrue if V_ALIGN indicates a curved road.is_truck_on_curveBooleanTrue only if both the vehicle is a truck AND the road is curved.
