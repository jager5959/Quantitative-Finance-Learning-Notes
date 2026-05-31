# data-cleaning
# use pandas to clean stock datas

## 读取 CSV 文件

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
