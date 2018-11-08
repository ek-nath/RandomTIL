## Running Jupyter notebooks on a server

1. Secure the jupyter server with a password
`jupyter notebook password`
3. Launch the notebook without GUI
`jupyter notebook --no-browser --port=8080`
2. Create SSH Tunnel
`ssh -N -L localhost:8888:localhost:8080 <username>@<server_ip>`

### Optional

1. Update `~/.ssh/config` to contain ssh login configuration like

```
Host remoteserver
    HostName <ip.add.re.ss>
    User <username>
```
2. Then you can `ssh -N -L localhost:8888:localhost:8080 remoteserver`

## Show formatted dataframe from the middle of jupyter cell

Many times we have situations like
```python
df = pd.DataFrame(..)
df.head()
df.col1.max()
```
This will only output the max value of `col1` without the output of `head()`
The `display` function from `IPython` solves that
```python
from IPython.display import display
df = pd.DataFrame(..)
display(df.head())
df.col1.max()
```
