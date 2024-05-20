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

- Using JetPack view bindings: to use object IDs in
  `activity_main.xml` directly within code, need some extra steps:


  - [In `build.gradle`](https://developer.android.com/topic/libraries/view-binding/migration):

    ```{kotlin}
    android {
        ...
        buildFeatures {
            viewBinding = true
        }
    }
    ```

  - [For elements in `activity_main.xml`, use `ActivityMainBinding` and "inflate" in `onCreate()`](https://developer.android.com/topic/libraries/view-binding#usage):

    ```{kotlin}
    private lateinit var binding: ActivityMainBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityMainBinding.inflate(layoutInflater)
        val view = binding.root
        setContentView(view)
    }
    ```

  - Then do stuff like this:

    ```{kotlin}
    binding.textview1.text = "hello"
    binding.button.setOnClickListener { viewModel.userClicked() }
    ```
