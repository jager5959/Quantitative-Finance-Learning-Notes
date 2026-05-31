# Python for Data Analysis
# use pandas to clean stock datas

## read CSV

```python
import pandas as pd

stock = pd.read_csv("dirty_stock_daily_ohlcv.csv")
```

## transform to datetime

```python
stock["date"] = pd.to_datetime(
    stock["date"],
    errors="coerce"
)
```

## delete repeated data

```python
stock = stock.drop_duplicates()
```

## find extreme price 
```python
extreme_price = (
    (stock["row_max_price"] > 3 * stock["median_close"]) |
    (stock["row_min_price"] < 0.3 * stock["median_close"])
)
```

## find extreme volume
```python
extreme_volume = (
    (stock["volume"] > 20 * stock["median_volume"]) |
    (
        (stock["volume"] > 0) &
        (stock["volume"] < 0.001 * stock["median_volume"])
    )
)
```

## delete unreasonable price

```python
stock = stock[
    (stock["open"] > 0) &
    (stock["high"] > 0) &
    (stock["low"] > 0) &
    (stock["close"] > 0) &
    (stock["volume"] >= 0)
]
```

## delete abnormal rows
```python
stock_clean = stock.loc[~abnormal_mask].copy()
```
