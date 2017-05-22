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


- As recommended by
  [Flask Web Development book](https://www.amazon.com/gp/product/1449372627?ie=UTF8&tag=7210-20),
  set up `virtualenv`. (Seems sort of like conda; maybe the same thing.)

  ```
  sudo apt-get install python-virtualenv

  virtualenv venv -p python3
  source venv/bin/activate
  ```

  Need to install all necessary modules (e.g. `pip install flask`).
  (Flask was already installed on my raspberry pi, but was not
  available within the virtual environment.)

  Back to normal with `deactivate`
