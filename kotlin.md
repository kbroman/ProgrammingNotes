## Kotlin

- `val` (immutable) vs `var` (variable)

   ```{kotlin}
   val max_iter = 1000
   var max_iter = 1000
   var max_iter : Long = 1000
   var name : String
   ```

- string templates

  ```{kotlin}
  "$name has ${output - input} net output"
  ```

- for loops

  ```{kotlin}
  val list = 1..10
  for(i in list) { }
  ```

- functions

  ```{kotlin}
  fun getSum(a: Int, b: Int): Int {
    return a + b
  }

  fun getSum(a: Int, b: Int) = a + b
  ```

- access a view element by id

  ```{kotlin}
  val textValue_view = findViewById<TextView>(R.id.textValue)
  textValue_view?.text = "hello"

  findViewById<Button>(R.id.buttonHide)?.setOnClickListener(this)
  ```
