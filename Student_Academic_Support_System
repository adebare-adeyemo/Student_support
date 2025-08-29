import streamlit as st
import pandas as pd
import joblib
import traceback

# Load pipeline (model + encoder combined)
pipeline = joblib.load(r"C:\Users\adeye\Downloads\Student_Risk_Advisor_Package\student_risk_pipeline_balanced.pkl")

st.set_page_config(page_title="Student Academic Support System", layout="wide")
st.title("🎓 Student Academic Support System ")

st.write("Fill in your academic and personal details to assess your risk level.")

# Input form
with st.form("student_form"):
    study_hours = st.selectbox("Study Hours", ["less than 1 hour", "1 - 2 hours", "3 - 4 hours", "more than 4 hours"])
    sleep_hours = st.selectbox("Sleep Hours", ["less than 4 hours", "4 - 6 hours", "6 - 8 hours", "more than 8 hours"])
    attendance = st.selectbox("Class Attendance", [
        "rarely (less than 50%)", "sometimes (50 - 69%)", "often (70 - 89%)", "always (90–100%)"
    ])
    peer_influence = st.selectbox("Peer Influence", ["never", "slightly", "moderate", "strong"])
    parental_involvement = st.selectbox("Parental Involvement", ["not involved at all", "somewhat involved", "very involved"])
    financial_difficulty = st.selectbox("Financial Difficulty", ["no", "yes, occasionally", "yes, frequently"])
    leisure_activities = st.selectbox("Leisure Activities", ["rarely", "sometimes", "often"])
    extracurricular = st.selectbox("Extracurricular Activities", ["none", "occasional", "frequent"])
    level = st.selectbox("Academic Level", ["100", "200", "300", "400", "500"])
    family_income = st.selectbox("Family Income", ["below ₦50,000", "₦50,000–₦100,000", "₦100,000–₦200,000", "above ₦200,000"])
    age = st.number_input("Age", min_value=15, max_value=40, step=1)
    past_question_study = st.selectbox("Past Question Study", ["yes", "no"])
    attention_in_class = st.selectbox("Attention in Class", ["very well", "sometimes", "rarely", "not at all"])
    parent_education = st.selectbox("Parent Education", [
        "none", "primary", "secondary", "diploma/nce", "undergraduate", "postgraduate (master's/phd)"
    ])
    parental_relationship = st.selectbox("Parental Relationship", ["married (living together)", "single parent", "divorced"])
    learning_difficulty = st.selectbox("Learning Difficulty", ["yes", "no"])
    cgpa = st.number_input("Current CGPA", min_value=0.0, max_value=5.0, step=0.01, value=3.0)

    submit = st.form_submit_button("Predict Risk")

if submit:
    try:
        # Prepare DataFrame with all inputs
        input_df = pd.DataFrame({
            "Study Hours": [study_hours],
            "Sleep Hours": [sleep_hours],
            "Class Attendance": [attendance],
            "Peer Influence": [peer_influence],
            "Parental Involvement": [parental_involvement],
            "Financial Difficulty": [financial_difficulty],
            "Leisure Activities": [leisure_activities],
            "Extracurricular": [extracurricular],
            "Level": [level],
            "Family Income": [family_income],
            "Age": [age],
            "Past Question Study": [past_question_study],
            "Attention in Class": [attention_in_class],
            "Parent Education": [parent_education],
            "Parental Relationship": [parental_relationship],
            "Learning Difficulty": [learning_difficulty],
            "CGPA": [cgpa]
        })

        # Predict probability
        probability = pipeline.predict_proba(input_df)[0][1]
        threshold = 0.3  # Lower threshold
        prediction = 1 if probability >= threshold else 0

        # Output results
        st.subheader("📊 Prediction Result")
        if prediction == 1:
            st.error(f"⚠️ You are AT RISK (Risk Score: {probability:.2f})")
            st.markdown("### 📝 Recommendations:")
            
            # Check all inputs for advice
            if cgpa < 2.0:
                st.write("- Your CGPA is low. Consider extra academic support.")
            if "less than 1 hour" in study_hours or "1 - 2 hours" in study_hours:
                st.write("- Increase your study time to at least 6 hours/week.")
            if "rarely" in attendance or "sometimes" in attendance:
                st.write("- Improve class attendance to above 80%.")
            if "less than 4 hours" in sleep_hours or "4 - 6 hours" in sleep_hours:
                st.write("- Improve your sleep hygiene for better focus.")
            if financial_difficulty == "yes, frequently":
                st.write("- Seek financial aid or counseling services.")
            if parental_involvement == "not involved at all":
                st.write("- Engage mentorship or counseling services.")
            if learning_difficulty == "yes":
                st.write("- Visit academic support services for learning assistance.")
        else:
            st.success(f"✅ You are NOT at risk (Risk Score: {probability:.2f})")
            st.markdown("### 👍 Keep it up:")
            st.write("- Maintain consistent study, sleep, and class habits.")
            st.write("- Keep a balanced academic and social life.")

    except Exception as e:
        st.error("❌ Something went wrong:")
        st.code(traceback.format_exc())
