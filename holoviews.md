## Selecting data from `Points` 

### Context
You can create `Points` out of a `dataframe`
```python
points = hv.Points(df, kdims=['col_a', 'col_b'])
# kdims are independent variables. 
# Note: `df` has more than just the independent variables.
```

Now we can filter data from this using a `select` query. Here we're selecting values in the range: [`None`, `10.0`]
`points.select(fare_amount=(None, 10.0))`

We can also `select` specific values: `points.select(fare_amount=(11.3))`
