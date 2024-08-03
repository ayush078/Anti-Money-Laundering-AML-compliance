# AML Compliance Example

This repository contains an example project for Anti-Money Laundering (AML) compliance. It includes sample code for transaction monitoring and KYC (Know Your Customer) verification, as well as guidance on running the code in Google Colab.

## Project Overview

This project demonstrates basic AML compliance techniques, including:
- Monitoring transactions for suspicious activities 
- Verifying customer KYC status
- Generating reports of suspicious transactions


# Transaction Monitoring: Identifies and flags suspicious transactions based on predefined thresholds.
# KYC Verification: Checks the KYC status of customers.
# Export Report: Generates a CSV report of suspicious transactions.
Example Google Colab notebook code:

import pandas as pd
from google.colab import files

# Upload files
uploaded = files.upload()

# Read data
transactions_df = pd.read_csv('transactions.csv')
customers_df = pd.read_csv('customers.csv')

# Transaction monitoring
threshold = 10000
transactions_df['Suspicious'] = transactions_df['Amount'] > threshold
suspicious_transactions = transactions_df[transactions_df['Suspicious']]
print("Suspicious Transactions:")
print(suspicious_transactions)

# KYC verification
def check_kyc(customer_id):
    customer = customers_df[customers_df['CustomerID'] == customer_id]
    if customer.empty:
        return "Customer not found."
    elif customer['DocumentVerified'].values[0]:
        return "KYC Verified."
    else:
        return "KYC Pending."

customer_id = 'C002'
print(f"Customer {customer_id} KYC Status: {check_kyc(customer_id)}")

# Export report
suspicious_transactions.to_csv('suspicious_transactions_report.csv', index=False)
print("Report generated successfully.")
