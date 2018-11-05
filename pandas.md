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
