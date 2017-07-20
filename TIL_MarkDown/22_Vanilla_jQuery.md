# Vanilla script  vs  jQuery library

## Vanilla Script

```javascript
((global, user) => {

  'use strict';

  let document = global.document;
  let user_input = null;
  let print_user_input = null;

  function init() {
    user_input = document.querySelector('.user-input');
    print_user_input = document.querySelector('.print-user-input');
    render();
    bind();
  }

  function bind() {
    user_input.addEventListener('keyup', update);
  }

  function render() {
    let msg = user.data.message;
    user_input.value = msg;
    print_user_input.textContent = msg;
  }

  function update(e) {
    let value = e.target.value;
    user.data.message = value;
    print_user_input.textContent = value;
  }

  init();

}) (window, window.user);
```

## jQuery Library

```javascript
((global, user, $) => {

  'use strict';

  let $user_input, $print_user_input;

  function init() {
    $user_input = $('.user-input');
    $print_user_input = $('.print-user-input');
    render();
    bind();
  }

  function bind() {
    $user_input.on('keyup', update);
  }

  function render() {
    let value = user.message;
    $user_input.val(value);
    $print_user_input.text(value);
  }

  function update(e) {
    let value = e.target.value;
    user.message = value; // Update State
    $print_user_input.text(value); // Update View
  }

  init();

}) (window, window.user, window.jQuery);
```