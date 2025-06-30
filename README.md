import streamlit as st
from datetime import datetime

st.title("💪 BMI & Health Report App")

# User Inputs
name = st.text_input("👤 Enter your name")
weight = st.number_input("⚖️ Enter your weight (kg)", min_value=1.0, step=0.5)
height = st.number_input("📏 Enter your height (cm)", min_value=50.0, step=0.5)

# Calculate BMI
if st.button("📊 Calculate BMI"):
    if weight and height:
        height_m = height / 100
        bmi = round(weight / (height_m ** 2), 2)

        # Determine BMI Category
        if bmi < 18.5:
            category = "Underweight"
            message = "⚠️ You are underweight."
        elif bmi <= 24.9:
            category = "Normal weight"
            message = "✅ You have a normal weight. Keep it up!"
        else:
            category = "Overweight"
            message = "⚠️ You are overweight."

        # Water intake suggestion
        water_intake = round(weight * 35)  # in ml

        # Show Results
        st.success(f"Hello {name}! 💖")
        st.info(f"Your BMI is: {bmi}")
        st.warning(message)
        st.write(f"💧 Suggested daily water intake: **{water_intake} ml**")

        # Prepare Health Report Text
        today = datetime.now().strftime("%d-%m-%Y")
        report = f"""
        Health Report for {name}
        Date: {today}

        Weight: {weight} kg
        Height: {height} cm
        BMI: {bmi}
        Category: {category}

        💧 Recommended Water Intake: {water_intake} ml/day

        Message: {message}
        """

        # Download Button
        st.download_button("📥 Download Health Report", report, file_name="health_report.txt")

    else:
        st.error("Please fill in all the details.")
