---
layout: article
title: Simple flask payload dump
categories: learning
modified: 2020-10-14T16:28:11-04:00
tags: [python, flask]
comments: true
share: true
read_time: true
---

I'm building an integration between two services and wanted to know what was being sent. This simple flask app allowed me to check the payload. Run this, and then open a ngrok tunnel connected to port 5000. You'll have a live incoming webhook app!

```
from flask import Flask, request
import pprint

app = Flask(__name__)

@app.route('/', methods=['POST']) 
def foo():
    print("incoming request headers: \n")
    print(request.headers)
    print("incoming request json payload: \n")
    maybe = request.get_json()
    print(pprint.pprint(maybe))
    return '', 200


if __name__ == "__main__":
    app.run(debug=True)
```