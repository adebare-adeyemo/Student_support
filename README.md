Student Academic Support System for Performance Improvement

✅ Tools & Frameworks Used

📦 Python Libraries

Tool	Purpose
pandas	Reading and managing tabular student data (CSV format)
scikit-learn	Machine learning model training (Gradient Boosting), preprocessing (OneHotEncoder), pipeline creation, model evaluation, and class balancing
joblib	Saving and loading the trained ML model and preprocessing pipeline
matplotlib / seaborn (optional)	Visualizing feature importance or performance metrics (ROC curve, etc.)
traceback	Capturing and displaying error messages in the app
numpy (used internally by sklearn/pandas)	Mathematical operations, arrays


⸻

🧠 Machine Learning Algorithm

Model	Purpose
Gradient Boosting Classifier	Core model used to classify students as “At Risk” or “Not At Risk” based on behavior, performance, and socio-economic features
class_weight='balanced'	Helps solve class imbalance (e.g. if only few students are “At Risk”)


⸻

🎛️ Preprocessing

Tool	Purpose
OneHotEncoder	Converts categorical features (like “Study Hours”) into machine-readable format
ColumnTransformer	Applies transformations (encoding) only to selected columns
Pipeline	Chains preprocessing + model into a single object to avoid mismatch during deployment


⸻

🧪 Model Evaluation

Metric	Purpose
Accuracy Score	Measures how many predictions were correct
ROC-AUC Score	Measures how well the model separates At Risk from Not At Risk students
Threshold Tuning (e.g. 0.3)	Custom threshold to make the model more sensitive to borderline students


⸻

🌐 Frontend / App Interface

Tool	Purpose
Streamlit	Web app framework to allow users to input student data and get predictions + recommendations in real-time
streamlit.sidebar.slider	Lets user dynamically adjust the risk classification threshold
PIL (optional)	Display visualizations like feature importance charts
Streamlit forms, selectbox, number_input	User interface components to collect structured data


⸻

💾 Deployment / Packaging

Tool	Purpose
requirements.txt	Lists all dependencies needed to run the app (for local use or Streamlit Cloud deployment)
joblib .pkl files	Serialized ML pipeline saved and reused in the app
Streamlit Cloud / Localhost	Hosting the app for user access


⸻

🧠 Optional (Advanced Enhancements)

Tool	Purpose
SHAP or LIME (optional)	Explainable AI tools to interpret model decisions (e.g., why student was flagged as “at risk”)
SMOTE (optional)	Synthetic oversampling of minority class (At Risk) to improve model learning
