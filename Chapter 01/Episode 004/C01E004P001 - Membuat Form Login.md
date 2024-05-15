# C01E004P001 - Membuat Form Login



resources\views\auth\login\index.blade.php

```html
<div class="container">
   <div class="row justify-content-center">
      <div class="col-lg-5">
         <div class="card shadow-lg border-0 rounded-lg mt-5">
            <div class="card-header">
               <h3 class="text-center font-weight-light my-4">Login</h3>
            </div>
            <div class="card-body">
               <form action="" method="POST">
                  <div class="form-floating mb-3">
                     <input name="email" class="form-control" id="inputEmail" type="email" placeholder="Enter email..."
                        autocomplete="username">
                     <label for="inputEmail">Email</label>
                  </div>
                  <div class="form-floating mb-3">
                     <input name="password" class="form-control" id="inputPassword" type="password" placeholder="Enter password..."
                        autocomplete="current-password">
                     <label for="inputPassword">Password</label>
                  </div>
                  <div class="d-flex align-items-center justify-content-between mt-4 mb-0">
                     <span>
                        <a class="small" href="/">Home</a> /
                        <a class="small" href="/">Forgot Password?</a>
                     </span>
                     <button type="submit" class="btn btn-primary">Login</button>
                  </div>
               </form>
            </div>
         </div>
      </div>
   </div>
</div>
```


