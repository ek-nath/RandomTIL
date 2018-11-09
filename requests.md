## Keep-alive
Instead of `requests.post(...)`, if you use:
```python
with requests.session() as s:
    s.post(...)
```
The http connection will be kept alive from the **client-side**
Note: It is important that the server supports `keep-alive`. For flask server, check [flask](./flask.md)
