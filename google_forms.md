## Google forms

### Deleting all responses when grayed out

- See [this
  script](https://support.google.com/docs/thread/79482415?hl=en&msgid=92321115)

  ```javascript
  function test() {
      var form = FormApp.openById('[form ID from URL here]');
      form.deleteAllResponses();
  }
  ```

- Go to sheet that corresponds to form

- Click "Extensions" and "Apps Script"

- Need to click "Deploy" and give it access to your account

- Then click Run
