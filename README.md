# LuxDevHQ-Week9-Assignment
I worked with real APIs For this week's assignment  to fetch,process and save data using Python.
## What I Did
**Parts 1 & 2** – I created synthetic staff data on Mockaroo, hosted the JSON on GitHub,then pulled it down with `requests` and saved it as `staff_data.csv`.

**Part 3** – I hit two endpoints from the DummyJSON API - products and carts.I converted the responses into DataFrames and exported them as CSV files.The carts data needed a bit of flattening since each cart had nested product lists.

## Files i generated
- `staff_data.csv`
- `dummyjson_products.csv`
- `dummyjson_carts.csv`

## Quick review
```python
import requests, pandas as pd

# Staff data from GitHub
df = pd.DataFrame(requests.get("https://raw.githubusercontent.com/...").json())
df.to_csv("staff_data.csv", index=False)

# Flatten carts
rows = []
for cart in requests.get("https://dummyjson.com/carts").json()["carts"]:
    for p in cart["products"]:
        rows.append({
            "cart_id": cart["id"],
            "user_id": cart["userId"],
            "product": p["title"],
            "quantity": p["quantity"]
        })
pd.DataFrame(rows).to_csv("dummyjson_carts.csv", index=False)
```
