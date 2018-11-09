## Enable server-side `keep-alive`
```python
from werkzeug.serving import WSGIRequestHandler

if __name__ == '__main__':
    WSGIRequestHandler.protocol_version = "HTTP/1.1"
    app.run(debug=True, port=8000, host='0.0.0.0')
```
For client-side check [requests](requests.md)
