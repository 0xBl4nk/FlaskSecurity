# Flask Blog
simple unstyled blog in Flask for security training on API, XSS, SQLI, etc...


- BLOG url: http://127.0.0.1:5000 and http://127.0.0.1:5000/test
- Requirements: flask, flask_sqlalchemy

## Api
```
API:
      List Posts: GET    http://127.0.0.1:5000/api/posts
       Add Posts: PUT    http://127.0.0.1:5000/api/posts     -> Format: {"title": "", "content": "", "author":""}
      Edit Posts: PUT    http://127.0.0.1:5000/api/post/<id> -> Format: {"title": "", "content": "", "author":""}
    Delete Posts: DELETE http://127.0.0.1:5000/api/post/<id>
```

## Security Code

```python
# TEST url: http://127.0.0.1:5000/test

@app.route('/test')
def test():
    name = request.args.get('name')
    response = make_response(f'Hello {name}')
    response.set_cookie('info', 'session123', httponly=True) # Don't show cookies on alert -> http=only
    return response
```

```python
# Owasp Security Headers

@app.after_request
def add_header(response):
    response.headers['X-Frame-Options'] = 'DENY'
    response.headers['Content-Security-Policy'] = 'script-src "none"'
    #response.headers['Access-Control-Allow-Origin'] = 'example.com' # *, domain, null -> OBS: may be unsafe in some cases
    #response.headers['Access-Control-Allow-Credentials'] = 'false'
    return response
```