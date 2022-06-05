## Client

```python
from binance import Client
%run ./Binance_keys.ipynb
client = Client(api_key=bnb_key, api_secret=bnb_secret)

```

## get_data
```python
def getminutedata(symbol, interval, lookback):
    frame = pd.DataFrame(client.get_historical_klines(symbol, interval, lookback + ' min ago UTC'))
    frame = frame.iloc[:,:6]
    frame.columns = ['Time', 'Open', 'High', 'Low', 'Close', 'Volume']
    frame = frame.set_index('Time')
    frame.index = pd.to_datetime(frame.index, unit='ms')
    frame = frame.astype(float)
    return frame
```

## BinanceSocket to SQLITE
```python
from binance import BinanceSocketManager

socket = bsm.trade_socket('CAKEBUSD')
def createframe(msg):
    df = pd.DataFrame([msg])
    df = df.loc[:,['s', 'E', 'p']]
    df.columns = ['symbol', 'Time', 'Price']
    df.Price = df.Price.astype(float)
    df.Time = pd.to_datetime(df.Time, unit = 'ms')
    return df
    
engine = sqlalchemy.create_engine('sqlite:///CAKEBUSDstream.db')

while True:
    await socket.__aenter__()
    msg = await socket.recv()
    frame = createframe(msg)
    frame.to_sql('CAKEBUSD', engine, if_exists = 'append', index = False)
    print(msg)
    
```

## applyindicators
```python
def applyindicators(df):
    df['SMA_200'] = df.Close.rolling(200).mean()
    df['SMA_20'] = df.Close.rolling(20).mean()
    df['stddev'] = df.Close.rolling(20).std()
    df['Upper'] = df.SMA_20 + 2 * df.stddev
    df['Lower'] = df.SMA_20 - 2 * df.stddev
    df['rsi'] = ta.momentum.rsi(df.Close, 2)
    return df
```

##

## get_top_symbol
```python
def get_top_symbol():
    all_pairs = pd.DataFrame(client.get_ticker())
    all_pairs['priceChangePercent'] = all_pairs['priceChangePercent'].astype('float')
    relev = all_pairs[all_pairs.symbol.str.endswith('BUSD')]
    non_lev = relev[~((relev.symbol.str.contains('UP')) | relev.symbol.str.contains('DOWN'))]
    top_symbol = non_lev[non_lev.priceChangePercent== non_lev.priceChangePercent.max()]
    print('priceChangePercent', str(top_symbol.priceChangePercent.values[0]))
    top_symbol = top_symbol.symbol.values[0]
    return top_symbol
```

## BUY order

```python
def buy(symbol, investment):
    order = client.order_limit_buy(
        symbol = symbol,
        price = pricecalc(symbol),
        quantity = quantitycalc(symbol, investment))
    changepos(symbol, order)
    print(order)
```

## SELL order

```python
def sell(symbol):
    order = client.create_order(
        symbol=symbol,
        side = 'SELL',
        type = 'MARKET',
        quantity = tradedf[trades.symbol == symbol].quantity.values[0]
    )
    changepos(symbol, order)
    print(order)
```

## Symbols
```python
symbols = ['ETHBUSD','BNBBUSD','XECBUSD','MATICBUSD','LUNABUSD', 'LUNCBUSD','SOLBUSD','EOSBUSD','BCHBUSD', 
           'ONEBUSD', 'GRTBUSD', 'AVAXBUSD', 'XLMBUSD','ETCBUSD','HBARBUSD','SANDBUSD','TRXBUSD','SHIBBUSD',
           'ATOMBUSD','FLOWBUSD','AXSBUSD','DOGEBUSD','GALABUSD','TFUELBUSD','CAKEBUSD', 'EGLDBUSD',           
           'AAVEBUSD', 'ALGOBUSD', 'KLAYBUSD','MANABUSD','ADABUSD','XRPBUSD','NEARBUSD','DOTBUSD','VETBUSD','FILBUSD', 
           'NEOBUSD','UNIBUSD','HNTBUSD','LTCBUSD','ICPBUSD','LINKBUSD','XMRBUSD','THETABUSD', 
           'ONTBUSD','XTZBUSD','FTTBUSD','MKRBUSD','ENJBUSD']
```
