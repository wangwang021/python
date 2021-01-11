# flask同源策略解决办法及flask-cors只允许特定域名跨域

falsk 同源策略解决办法：

使用 flask-cors 包 并且 在代码里 加响应的一行代码解决。

```python
from flask import Flask, session
from flask_cors import CORS

app = Flask(__name__)
CORS(app,  resources={r"/*": {"origins": "*"}})   # 允许所有域名跨域

@app.route("/")
def helloWorld():
  return "Hello, %s" % session['username']


from flask import Flask, session
from flask_cors import CORS

app = Flask(__name__)
cors = CORS(app, resources={r"/.*": {"origins": "http://192.168.1.92:8081"}})   # 只允许特定域名跨域

@app.route("/")
def helloWorld():
  return "Hello, %s" % session['username']
from flask import Flask, session
from flask_cors import CORS

app = Flask(__name__)
cors = CORS(app, resources={r"/.*": {"origins": ["http://192.168.1.92:8081","http://www.bai.com"]}})   # 只允许特定几个域名跨域

@app.route("/")
def helloWorld():
  return "Hello, %s" % session['username']
```

