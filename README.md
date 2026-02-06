# SolarWaterFlow-
SolarWaterFlow – AI agent guiding smart water and solar energy decisions."
import streamlit as st
import numpy as np
import matplotlib.pyplot as plt

# ----------------------------------
# AI Prediction Functions
# ----------------------------------

# Predict solar energy based on temperature and sunlight hours
def predict_solar_energy(temperature, sunlight_hours):
    return 0.5 * sunlight_hours * temperature

# Predict water demand based on temperature and population
def predict_water_demand(temperature, population):
    return 0.3 * population * temperature

# AI Decision Agent
def system_recommendation(solar_energy, water_demand):
    if solar_energy > water_demand * 0.01:
        return "✅ System Decision: Solar energy is sufficient to supply water demand."
    else:
        return "⚠️ System Decision: Energy is insufficient. Consider storage or demand reduction."

# ----------------------------------
# Streamlit App Interface
# ----------------------------------

st.set_page_config(page_title="SolarWaterFlow AI Agent", layout="centered")
st.title("🌞💧 Smart Water and Energy Management System")

st.write(
    "This AI-driven system evaluates solar energy production and water demand "
    "and provides intelligent recommendations for sustainable resource management."
)

# ----------------------------------
# User Inputs
# ----------------------------------

temperature = st.slider(
    "🌡️ Enter the temperature (°C)",
    min_value=0,
    max_value=40,
    step=1
)

sunlight_hours = st.slider(
    "☀️ Enter the sunlight hours per day",
    min_value=0,
    max_value=12,
    step=1
)

population = st.slider(
    "👥 Enter the population size",
    min_value=100,
    max_value=10000,
    step=100
)

# ----------------------------------
# Prediction Button
# ----------------------------------

if st.button("🔍 Run AI Analysis"):
    solar_energy = predict_solar_energy(temperature, sunlight_hours)
    water_demand = predict_water_demand(temperature, population)
    decision = system_recommendation(solar_energy, water_demand)

    # Results
    st.subheader("📊 AI Predictions")
    st.write(f"Estimated Solar Energy Production: **{solar_energy:.2f} kWh**")
    st.write(f"Estimated Water Demand: **{water_demand:.2f} liters/day**")

    # AI Decision
    st.subheader("🧠 AI System Decision")
    if "sufficient" in decision:
        st.success(decision)
    else:
        st.warning(decision)

    # ----------------------------------
    # Visualization
    # ----------------------------------

    fig, ax = plt.subplots(1, 2, figsize=(10, 5))

    ax[0].bar(["Solar Energy"], [solar_energy])
    ax[0].set_title("Solar Energy Production (kWh)")
    ax[0].set_ylabel("Energy (kWh)")

    ax[1].bar(["Water Demand"], [water_demand])
    ax[1].set_title("Water Demand (liters/day)")
    ax[1].set_ylabel("Water (liters)")

    st.pyplot(fig)
