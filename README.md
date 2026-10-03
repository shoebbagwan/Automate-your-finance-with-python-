Personal Finance Dashboard

An interactive finance dashboard built with Streamlit, Pandas and Plotly. Upload a bank or credit card statement CSV and the app cleans the data, separates expenses from payments, auto-categorises transactions using keyword rules, and visualises your spending.

Everything runs locally, so your statements stay on your machine.

Project Details
Automatic data cleaning: trims column names, parses dates, and converts amounts with commas, currency symbols, negatives or (parentheses) into numbers
Expenses vs. payments: debits and credits are split into separate tabs so card payments don't inflate your spending
Rule-based categorisation: transaction descriptions are matched against keywords stored in categories.json
Inline editing: change a category from a dropdown, click Apply & Save Changes, and the app learns the merchant for future uploads
Custom categories: add your own, such as Groceries, Rent or Fuel
Analytics: category summary table, interactive pie chart, and metric cards for total expenses, total payments and uncategorised items
Error handling: clear messages for empty files, missing columns, unreadable dates or amounts, and a corrupted categories.json
Tech Stack
Purpose	Tool
Language	Python 3.10+
UI framework	Streamlit
Data processing	Pandas
Visualisation	Plotly Express
Rule storage	Local categories.json
Usage
Installation
bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>

pip install -r requirements.txt
Run the app
bash
streamlit run app.py

The app opens at http://localhost:8501.

Using the dashboard
Upload your bank statement CSV.
Check the metric cards: total expenses, payments received, and uncategorised count.
In the Expenses (Debits) tab, find rows marked Uncategorized, pick a category from the dropdown, and click Apply & Save Changes.
Use Add a new category to create your own categories.
Scroll down for the summary table and pie chart. Click legend items to hide or show categories.
Open the Payments & Income (Credits) tab to see card payments and money received.
CSV format
Column	Required	Notes
Date	Yes	e.g. 28-Feb-25, 28/02/2025, 2025-02-28
Details	Yes	Merchant or description (Description also works)
Amount	Yes	Commas, currency symbols and negatives are handled
Debit/Credit	No	If missing, negative amounts are treated as debits
Currency	No	Used for display, e.g. AED

Example:

csv
Date,Details,Amount,Currency,Debit/Credit,Status
28-Feb-25,Card Payment,"18,551.62",AED,Credit,SETTLED
05-Oct-24,LULU HYPERMARKET,455,AED,Debit,SETTLED
14-Jan-25,UBER AE,105.84,AED,Debit,SETTLED
How categorisation works

categories.json is created automatically on first run and maps each category to keywords:

json
{
    "Shopping": ["noon", "amazon", "lulu"],
    "Travel": ["uber", "careem", "emirates"],
    "Uncategorized": []
}

A transaction gets the category whose keyword appears in its description (the longest match wins). Anything unmatched stays Uncategorized. When you save an edit, the description is added as a keyword so future uploads are categorised automatically.
