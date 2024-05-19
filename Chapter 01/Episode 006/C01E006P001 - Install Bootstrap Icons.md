# C01E006P001 - Install Bootstrap Icons

## Install Bootstrap Icons

```bash
npm install bootstrap-icons@^1.11.3 --save-dev
```

## Config SASS

resources\sass\vendors\_icons.scss

```sass
$bootstrap-icons-font-dir: "bootstrap-icons/font/fonts";
@import "bootstrap-icons/font/bootstrap-icons.scss";
```

resources\sass\app.scss

```sass
//@import "./helpers";
//@import "./utilities";

// vendor
@import "./vendors/icons";
```

## Test Icon

```html
<i class="bi bi-box-arrow-in-right"></i>
```

## Ref

- https://icons.getbootstrap.com/
