# Diabetes Prediction App

## Overview
The Diabetes Prediction App is a Streamlit application that collects clinical input features, loads pre-trained machine-learning models, predicts a diabetes-related outcome, and stores the inputs and predictions in a MongoDB Atlas collection. The repository contains the Streamlit app, a MongoDB connection test script, and a requirements file.

## Features
- Interactive Streamlit UI for entering clinical features and getting real-time predictions.
- Two model predictions (Ridge and Lasso) loaded from pickle files.
- Input + prediction persistence in a MongoDB Atlas database/collection for later analysis.
- A standalone MongoDB ping/test script to verify connectivity.

## Technologies Used
- Python
- Streamlit
- scikit-learn (models)
- pandas
- NumPy
- pickle (for model serialization)
- MongoDB (pymongo)

## Requirements
Install the packages listed in requirements.txt. The included requirements file lists scikit-learn and pymongo; add any missing packages (streamlit, pandas, numpy, etc.) if not present in your requirements file.

Example:
pip install -r requirements.txt

Recommended dependencies to include:
- streamlit
- pandas
- numpy
- scikit-learn
- pymongo

## Files in this Repository
- diabetes_prediction.py - Streamlit application: collects user inputs, loads models & scalers, preprocesses inputs, runs predictions, and inserts records into MongoDB.
- mongodb_connect.py - Simple script that creates a MongoClient and sends a ping to confirm Atlas connectivity (useful to test your URI and network access).
- requirements.txt - Declared Python dependencies (currently includes scikit-learn and pymongo).
- diabetes_ridge_final_model.pkl - Expected Ridge model pickle (should contain model and scaler) - required by the app.
- diabetes_lasso_final_model.pkl - Expected Lasso model pickle (should contain model and scaler) - required by the app.

Make sure the pickle model files are present in the same directory as the app or update file paths in the code.

## MongoDB Connection
The app connects to MongoDB Atlas using a connection URI variable present in the code. Before running the app, update the URI to use your credentials or (preferably) load it from an environment variable or secrets manager. Do NOT commit credentials to source control. The repository includes a separate script to verify connectivity via a ping command.

Best practice:
- Store the URI in an environment variable (for example, MONGODB_URI) and read it in the code.
- Ensure your Atlas IP access list allows connections from your environment.

## Inputs (UI fields)
The Streamlit app collects the following inputs as numeric fields (as defined in the code). These correspond to the features expected by the pre-trained models; do not change their order unless you also update the preprocessing and models:
- Age
- Sex/Gender
- BMI (Body Mass Index)
- ABP (Average Blood Pressure)
- S1 (Total Serum Cholesterol)
- S2 (Low-Density Lipoproteins)
- S3 (High-Density Lipoproteins)
- S4 (Total Cholesterol/HDL)
- S5 (Possibly log of serum triglycerides level)
- S6 (Blood Sugar Level)
These inputs are created as Streamlit number_input fields in the app.

## How to Run
1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/diabetes-prediction-app.git
   ```
   ```bash
   cd diabetes-prediction-app
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
   (Add streamlit, pandas, numpy if they are not in requirements.txt.)

3. Ensure model pickle files (diabetes_ridge_final_model.pkl and diabetes_lasso_final_model.pkl) are in the project directory.

4. Provide your MongoDB URI securely (environment variable or update the code temporarily for local testing).

5. Run the Streamlit app:
   ```bash
   streamlit run diabetes_prediction.py
   ```

6. (Optional) Test MongoDB connectivity:
   ```bash
   python mongodb_connect.py
   ```
   This script pings your Atlas deployment to confirm the connection.

## Usage
- Launch the app in your browser via Streamlit.  
- Fill the numeric fields listed above.  
- Click the prediction button to obtain results from Ridge and Lasso models. The app displays both prediction outputs and (if implemented) saves the input + predictions to the MongoDB collection.

## Data Storage
The app uses a MongoDB database and collection (created/used in the code). By default the code references a database and collection for diabetes predictions; you may rename them if desired. Inputs and prediction results are stored as documents for later querying and analysis.

## Troubleshooting
- If model loading fails, confirm that the pickle files exist and were produced with compatible Python and scikit-learn versions.  
- If MongoDB connection fails, confirm the URI, network access (Atlas IP whitelist), and use mongodb_connect.py to test the connection.
- If any required package is missing at runtime, add it to requirements.txt and reinstall dependencies.

## Contributing
Contributions are welcome. Suggested workflow:
- Fork the repo.
- Create a feature branch.
- Implement changes and update README and requirements.
- Open a pull request describing the changes.

## License
This project is licensed under the MIT License - see the LICENSE file for details.