# C01E016P001 - Notification (Toaster)

## Toaster (PHP)

app\Support\Toaster.php

```php
<?php

namespace App\Support;

use Illuminate\Support\Facades\Session;

class Toaster
{
    static string $key = 'toaster';

    public static function make($title, $message, $type = 'primary')
    {
        Session::push(self::$key, [
            'title' => $title,
            'message' => $message,
            'type' => $type,
        ]);
    }
    public static function success($title, $message)
    {
        self::make($title, $message, 'success');
    }
    public static function info($title, $message)
    {
        self::make($title, $message, 'info');
    }
    public static function warning($title, $message)
    {
        self::make($title, $message, 'warning');
    }
    public static function error($title, $message)
    {
        self::make($title, $message, 'danger');
    }
}
```

## Toaster (JS)

resources\js\plugins\toaster.js

```javascript
import { Toast } from "bootstrap";

const TOAST_TYPE = {
    PRIMARY: "PRIMARY",
    INFO: "INFO",
    SUCCESS: "SUCCESS",
    WARNING: "WARNING",
    DANGER: "DANGER",
};

const TOAST_ICON = {
    PRIMARY: "bi-bell text-primary",
    INFO: "bi-info-square text-info",
    SUCCESS: "bi-check-square text-success",
    WARNING: "bi-exclamation-triangle text-warning",
    DANGER: "bi-exclamation-square text-danger",
};

const DEFAULT_DELAY = 5000;

const DEFAULT_ANIMATION = true;

const TOAST_TEMPLATE = `
<div class="toast" role="alert" aria-live="assertive" aria-atomic="true">
   <div class="toast-header border-bottom-0">
      <i id="toastIcon" class="bi me-2 rounded fs-6"></i>
      <strong id="toastTitle" class="me-auto">%TITLE%</strong>
      <button type="button" class="btn-close" data-bs-dismiss="toast" aria-label="Close"></button>
   </div>
   <div id="toastMessage" class="toast-body">
      %MESSAGE%
   </div>
</div>
`;

class Toaster {
    constructor(config = { idContainer: "toastContainer", option: {} }) {
        this.option = {
            delay: DEFAULT_DELAY,
            animation: DEFAULT_ANIMATION,
            ...config.option,
        };
        const idContainer = config.idContainer ?? "toastContainer";
        this.toastContainer = document.getElementById(idContainer);

        if (!this.toastContainer) {
            console.error("Toast container element not found.");
        }
        this.templateNode = this.createToastNode();
    }

    showToastNode(element = null) {
        const title = element.getAttribute("data-title");
        const message = element.getAttribute("data-message");
        const type = element.getAttribute("data-type");
        const toastNode = this.templateNode.cloneNode(true);
        toastNode
            .querySelector("#toastIcon")
            .classList.add(...TOAST_ICON[type]?.split(" "));
        toastNode.querySelector("#toastTitle").innerHTML = title;
        toastNode.querySelector("#toastMessage").innerHTML = message;
        this.render(toastNode);
    }

    createToastNode() {
        return new DOMParser().parseFromString(TOAST_TEMPLATE, "text/html").body
            .childNodes[0];
    }

    create(title, message, type = TOAST_TYPE.PRIMARY) {
        const toastNode = this.templateNode.cloneNode(true);
        toastNode
            .querySelector("#toastIcon")
            .classList.add(...TOAST_ICON[type]?.split(" "));
        toastNode.querySelector("#toastTitle").innerHTML = title;
        toastNode.querySelector("#toastMessage").innerHTML = message;
        this.render(toastNode);
    }

    show(title, message) {
        this.create(title, message, TOAST_TYPE.PRIMARY);
    }

    success(title, message) {
        this.create(title, message, TOAST_TYPE.SUCCESS);
    }

    info(title, message) {
        this.create(title, message, TOAST_TYPE.INFO);
    }

    warning(title, message) {
        this.create(title, message, TOAST_TYPE.WARNING);
    }

    error(title, message) {
        this.create(title, message, TOAST_TYPE.DANGER);
    }

    render(toastNode) {
        this.toastContainer.appendChild(toastNode);
        const length = this.toastContainer.querySelectorAll(".toast").length;
        if (length <= 7) {
            toastNode.addEventListener("hidden.bs.toast", () => {
                toastNode.remove();
            });
            const toast = new Toast(toastNode, {
                ...this.option,
                delay: parseInt(this.option.delay + (length - 1) * 500),
            });
            toast.show();
        }
    }
}

const toaster = new Toaster();

const loadToaster = () => {
    const toastTemporary = document.getElementById("toastTemporary");
    if (!toastTemporary) {
        console.error("Toast temporary element not found.");
        return;
    }
    const toastElList = toastTemporary.querySelectorAll(`div`);
    toastElList.forEach((toastEl) => {
        const clonedToast = toastEl.cloneNode(true);
        toaster.showToastNode(clonedToast);
        toastEl.remove();
    });
};

export { toaster, loadToaster, TOAST_TYPE };
```

## View

resources\views\toaster\toasts.blade.php

```php
@php
   $toasters = session()->has('toaster') ? session()->get('toaster') : [];
   $toasterConfig = config('toaster');
@endphp
<div aria-live="polite" aria-atomic="true" class="position-relative">
   <div class="d-none" id="toastTemporary">
      @foreach ($toasters as $toaster)
         @if ($loop->iteration <= 7)
            <div data-title="{{ $toaster['title'] }}" data-message="{{ $toaster['message'] }}"
               data-type="{{ strtoupper($toaster['type']) }}"></div>
         @else
         @break
      @endif
   @endforeach
</div>
<div id="toastContainer" class="toast-container p-3 top-0 end-0">
</div>

</div>
@if (session()->has('toaster'))
{{ session()->forget('toaster') }}
@endif
```

## Config (Dasboard)

resources\js\toaster.js

```javascript
import { loadToaster } from "../plugins/toaster";

window.addEventListener("DOMContentLoaded", () => {
    loadToaster();
    // another code...
});
```

resources\views\layouts\dashboard\dashboard-layout.blade.php

```php
<body class="sb-nav-fixed">
   @include('toaster.toasts')
   {{-- another code --}}
</body>
```

## Example

app\Http\Controllers\Dashboard\TagController.php

```php
<?php

namespace App\Http\Controllers\Dashboard;

//
use App\Support\Toaster;
//

class TagController extends Controller
{
    public function index(Request $request)
    {
        // anoter code 
        Toaster::make('Title','Message');
        return // anoter code;
    }

}
```

## Ref

- https://github.com/mckenziearts/laravel-notify

- https://github.com/philipp-winterle/bs-toaster

- https://github.com/PeytonRG/BootstrapToaster

- https://www.designcise.com/web/tutorial/how-to-remove-all-elements-returned-by-javascripts-queryselectorall-method
