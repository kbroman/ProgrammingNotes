## Flask

- At the top of the script, need `from flask import Flask`

  Then use `app = Flask(__name__)`

- Set up routes with `@app.route('/something')` and a handler function.

  ```
  @app.route("/')
  def index():
      return 'Hello, world!'
  ```

- HTML templates placed in `templates/`. Need
  `from flask import render_template` and then use
  `render_template('index.html')`

- CSS files placed in `static/`

- Use `<variable>` for variables in the URL. Inside a template,
  they'll be used as `{{ variable }}`. Within the python app, they're
  just a plain variable.

  ```
  @app.route('/hello/<name>')
  def hello(name):
      return "Hello, " + name
  ```

- At the bottom of the script,

  ```
  if __name__ == '__main__':
      app.run(debug=TRUE, host='0.0.0.0')
  ```

  The `host='0.0.0.0'` bit makes it accessible from other computers.
