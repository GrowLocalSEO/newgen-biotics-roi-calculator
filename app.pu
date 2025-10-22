import math
import streamlit as st
import pandas as pd
import matplotlib.pyplot as plt

st.set_page_config(page_title="ROI Calculator", layout="wide")

machines = st.sidebar.number_input("Number of Machines", min_value=1, value=1, step=1)
daily_income = st.sidebar.number_input("Daily Extra Income ($)", min_value=0.0, value=10.0)

equipment_cost = 3500
watts = 12
elec_rate = 0.35
days_per_month = 30
refill_cost = 250
months = 120

kw = watts / 1000
monthly_elec_cost = kw * 24 * elec_rate * days_per_month
monthly_income = daily_income * days_per_month
monthly_expenses = monthly_elec_cost + refill_cost
net_profit_per_machine = monthly_income - monthly_expenses
net_profit_all = net_profit_per_machine * machines

break_even = equipment_cost / net_profit_per_machine if net_profit_per_machine > 0 else math.inf
total_break_even = (equipment_cost * machines) / net_profit_all if net_profit_all > 0 else math.inf

st.title("New-Gen Biotics ROI Calculator")

# Chart
mths = list(range(1, months+1))
cum_profit = [(net_profit_all * m) - (equipment_cost * machines) for m in mths]
fig, ax = plt.subplots()
ax.plot(mths, cum_profit)
ax.set_xlabel("Months")
ax.set_ylabel("Cumulative Profit ($)")
st.pyplot(fig)

# Summary
st.subheader("Variable Summary")
st.write(f"Number of Machines: {machines}")
st.write(f"Total Monthly Income: ${monthly_income*machines:,.2f}")
st.write(f"Total Monthly Expenses: ${monthly_expenses*machines:,.2f}")
st.write(f"Net Monthly Profit: ${net_profit_all:,.2f}")
st.write(f"Break Even (per machine): {break_even:.1f} months")
st.write(f"Time to Pay Back All Machines: {total_break_even:.1f} months")
