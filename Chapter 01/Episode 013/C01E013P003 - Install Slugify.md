# C01E013P003 - Install Slugify (NPM)

```bash
npm install slugify@^1.6.6 --save-dev
```

resources\js\plugins\slugify.js

```js
import slugify from "slugify";

const generateSlug = (slug) => {
  return slugify(slug, {
    replacement: "-", // replace spaces with replacement character, defaults to `-`
    remove: undefined, // remove characters that match regex, defaults to `undefined`
    lower: false, // convert to lower case, defaults to `false`
    strict: false, // strip special characters except replacement, defaults to `false`
    locale: "vi", // language code of the locale to use
    trim: true, // trim leading and trailing replacement chars, defaults to `true`
  });
};

export { generateSlug };
```

resources\js\views\dashboard\tag\create.view.js

```js
import { generateSlug } from "../../../plugins/slugify";

function handleSlug() {
  const inputTitle = document.getElementById("inputTitle");
  const inputSlug = document.getElementById("inputSlug");
  const textSlug = document.getElementById("textSlug");
  inputTitle.addEventListener("change", (event) => {
    const title = event.target.value;
    const slug = generateSlug(title);
    inputSlug.value = slug;
    textSlug.innerText = slug;
  });
}

window.addEventListener("DOMContentLoaded", () => {
  //
  handleSlug();
  //
});
```

## Ref

- https://www.npmjs.com/package/slugify
