## Notes on Maxima

- created `/usr/local/bin/maxima` which contains

  ```
  exec '/Applications/Maxima.app/Contents/Resources/maxima.sh'
  ```

- Exit maxima with `quit();`

- Derivative

  ```
  diff( (z+8*r*y+2*(2*r+1)*x)/(3*(4*r+1)), r);
  ```

- Solve equation

  ```
  solve( [R = 1/8 - 1/8*(1-r)^3/(1+2*r)], [r]);
  ```

- Assign something a name with `:` for example

  ```
  y : log(x/(1-x));
  ```

- Simplify an expression with `radcan();`. For example:

  ```
  y : log(x/(1-x));
  z : diff(y, x);
  radcan(z);
  ```
