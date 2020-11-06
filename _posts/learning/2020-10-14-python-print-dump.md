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

First, let's create a virtual environment and install Flask.  After CDing into your work folder:

```bash
~ $ python3 -m venv virtualenvname
~ $ source virtualenvname/bin/activate  # for Linux & Mac
(virtualenvname) ~ $ pip3 install flask
```

Then, you can save this script in a `.py` file with a name you'd like such as `events.py`:

```python
from flask import Flask, request
import pprint

app = Flask(__name__)

@app.route('/', methods=['POST']) 
def foo():
    print("incoming request headers: \n")
    print(request.headers)
    print("incoming request json payload: \n")
    json_payload = request.get_json()
    print(pprint.pprint(json_payload))
    return '', 200


if __name__ == "__main__":
    app.run(debug=True)
```

To do this more "real" let's open a tunnel via ngrok on port 5000. Then, from Postman or curl, you can POST to this endpoint with some json data:

```bash
~$ curl --location --request POST 'https://{ngrokSubdomain}.ngrok.io' \
--header 'Content-Type: application/json' \
--data-raw '{"json":"data", "more":"info"}'
```

In the terminal where you were running the Flask app, you'll see:

```bash
$ python3 events.py 
 * Serving Flask app "events" (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: on
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 917-572-642
incoming request headers: 

Content-Type: application/json
User-Agent: PostmanRuntime/7.26.5
Accept: */*
Postman-Token: fabb1b81-fa4f-4829-bc1e-30321---
Host: {ngrokSubdomain}.ngrok.io
Accept-Encoding: gzip, deflate, br
Content-Length: 30
X-Forwarded-Proto: https
X-Forwarded-For: 3.93.254.1--


incoming request json payload: 

{'json': 'data', 'more': 'info'}
None
127.0.0.1 - - [06/Nov/2020 14:17:35] "POST / HTTP/1.1" 200 -
```


`{'json': 'data', 'more': 'info'}` is the json we sent in the POST request.

