## Resample a time-series indexed dataframe and perform aggregations

```python
>>> df.index

DatetimeIndex(['2017-06-01 14:24:03', '2017-06-09 17:38:10',
               '2017-06-09 18:57:53', '2017-06-20 18:45:36',
               '2017-06-22 17:38:38', '2017-06-26 17:35:15',
               '2017-06-27 16:26:32', '2017-06-28 16:49:03',
               '2017-06-29 10:30:40', '2017-06-29 11:00:22',
               ...
               '2017-06-30 16:03:12', '2017-06-30 16:12:44',
               '2017-06-30 16:23:22', '2017-06-30 16:32:28',
               '2017-06-30 16:43:05', '2017-06-30 16:53:29',
               '2017-06-30 17:02:28', '2017-06-30 17:13:05',
               '2017-06-30 17:22:54', '2017-06-30 17:32:26'],
              dtype='datetime64[ns]', name='Timestamp', length=6730856, freq=None)

>>> df.dtypes

Client_ID      object
PayloadSize     int64
dtype: object

>>> df.head()
                     Client_ID  PayloadSize
Timestamp                                  
2017-06-01 14:24:03  MTABC_185          514
2017-06-09 17:38:10  MTABC_185          511
2017-06-09 18:57:53  MTABC_185          531
2017-06-20 18:45:36  MTABC_185          528
2017-06-22 17:38:38  MTABC_185          517

>>> pd.DataFrame(df.groupby('Client_ID').resample('H')['PayloadSize'].sum())

                               PayloadSize
Client_ID Timestamp                       
MTABC_185 2017-06-01 14:00:00          514
          2017-06-01 15:00:00            0
          2017-06-01 16:00:00            0
          2017-06-01 17:00:00            0
          2017-06-01 18:00:00            0


```

## Rich-plotting

```python
import hvplot.pandas
data.hvplot()
```

## Percentile calculations on a row

Data:
```bash
                             1          2          3          4          5
Timestamp                                                                 
2018-11-05 06:00:00  13.624345  11.583242  13.788628  12.050562  12.441227
2018-11-05 07:00:00  13.584396  14.139886  14.632662  14.696104  13.865282
2018-11-05 08:00:00  14.471828  12.863804  15.096497  14.004091  17.430771
2018-11-05 09:00:00  13.123184  15.836423  12.332660  14.889751  13.944060
2018-11-05 10:00:00  12.865408  10.206564  11.722612  11.581698  12.109610
```
```python
df['99th percentile'] = df[[1, 2, 3, 4, 5].apply(lambda x: numpy.percentile(x, 99), axis=1)
```

## Create multiple new columns from one `apply`

```python
def add_subtract_series(a, b):
  return pd.Series((a + b, a - b))

df[['sum', 'difference']] = df.apply(
    lambda row: pd.Series(add_subtract(row['a'], row['b'])), axis=1)
```

Taken from [here](https://apassionatechie.wordpress.com/2017/12/27/create-multiple-pandas-dataframe-columns-from-applying-a-function-with-multiple-returns/)
