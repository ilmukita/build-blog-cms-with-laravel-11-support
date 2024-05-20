# C01E007P003 - Menambahkan Fungsi Logout

resources\views\layouts\dashboard_navbar.blade.php

```php
<li><a id="actionLogout" class="dropdown-item" href="#">Logout</a></li>
<form id="formLogin" action="{{ @route('auth.logout') }}" method="POST">
   @csrf
</form>
```

resources\js\layouts\dashboard.js

```js
function actionLogout() {
    const linkLogin = document.getElementById("actionLogout");
    const formLogin = document.getElementById("formLogin");

    linkLogin.addEventListener("click", () => {
        formLogin.submit();
    });
}
```

```js
window.addEventListener("DOMContentLoaded", () => {
    // another code...
    actionLogout();
});
```
