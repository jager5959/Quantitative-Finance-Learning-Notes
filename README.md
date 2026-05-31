# data-cleaning
# 使用 pandas 清洗股票数据

## 读取 CSV 文件

```python
import pandas as pd

stock = pd.read_csv("dirty_stock_daily_ohlcv.csv")
```

## 转换日期格式

```python
stock["date"] = pd.to_datetime(
    stock["date"],
    errors="coerce"
)
```

## 删除不合理的价格

```python
stock = stock[
    (stock["open"] > 0) &
    (stock["high"] > 0) &
    (stock["low"] > 0) &
    (stock["close"] > 0) &
    (stock["volume"] >= 0)
]
```
