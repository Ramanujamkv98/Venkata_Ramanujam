import pandas as pd
import numpy as np

def calculate_par(df):
    # df columns: ['item_id', 'issue_qty', 'direct_purchase', 'par_location']

    df['seven_day_demand'] = (df['issue_qty'] + df['direct_purchase']) / 7
    df['safety_stock'] = df['seven_day_demand'] * 1.5
    df['optimal_par'] = df['seven_day_demand'] + df['safety_stock']

    return df[['item_id', 'par_location', 'optimal_par']]

# Example
data = {
    'item_id': ['A1', 'B4', 'C8'],
    'issue_qty': [14, 70, 28],
    'direct_purchase': [0, 14, 7],
    'par_location': ['OR1', 'OR2', 'ED1']
}

df = pd.DataFrame(data)
print(calculate_par(df))
