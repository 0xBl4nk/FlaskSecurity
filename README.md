BLOG url: http://127.0.0.1:5000

- Requirements: flask, flask_sqlalchemy

```
API:
      List Posts: GET    http://127.0.0.1:5000/api/posts
       Add Posts: PUT    http://127.0.0.1:5000/api/posts     -> Format: {"title": "", "content": "", "author":""}
      Edit Posts: PUT    http://127.0.0.1:5000/api/post/<id> -> Format: {"title": "", "content": "", "author":""}
    Delete Posts: DELETE http://127.0.0.1:5000/api/post/<id>
```

```python
# TEST url: http://127.0.0.1:5000/test

# Don't show cookies on alert -> http=only
@app.route('/test')
def test():
    name = request.args.get('name')
    response = make_response(f'Hello {name}')
    response.set_cookie('info', 'session123', httponly=True)
    return response
```

```python
# Owasp Security

@app.after_request
def add_header(response):
    response.headers['X-Frame-Options'] = 'DENY' # Denny Iframe's
    response.headers['Content-Security-Policy'] = 'script-src "none"' # Deny JS scripts
    return response
```