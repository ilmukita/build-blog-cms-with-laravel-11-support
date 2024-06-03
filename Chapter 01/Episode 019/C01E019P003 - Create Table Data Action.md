# C01E019P003 - Create Table Data Action

## Add Function Create Table Data Action

resources\js\plugins\dataTable.js

```js
import { bootstrap } from "./bootstrap";
```

```js
/**
 * Creates an icon element with a given name.
 * @param {string} name - The Bootstrap icon name.
 * @returns {HTMLElement} - The created icon element.
 */
const createIcon = (name) => {
    const iconEl = document.createElement("i");
    iconEl.classList.add("bi", name);
    return iconEl;
};

/**
 * Creates a button action element with specified options.
 * @param {Object} opts - Options for creating the button action.
 * @param {string} [opts.text="button"] - The text to display on the button.
 * @param {string} [opts.name="buttonAction"] - The name of the button action.
 * @param {string} [opts.icon=""] - The Bootstrap icon name to display on the button.
 * @param {string} [opts.className="btn-primary"] - Additional classes for the button.
 * @returns {HTMLButtonElement} - The created button action element.
 */
const createButtonAction = (opts = {}) => {
    const {
        text = "button",
        name = "buttonAction",
        icon = "",
        className = "btn-primary",
    } = opts;
    const buttonEl = document.createElement("button");
    if (icon) {
        buttonEl.append(createIcon(icon));
        buttonEl.dataset.bsToggle = "tooltip";
        buttonEl.dataset.bsPlacement = "top";
        buttonEl.dataset.bsTitle = text;
        bootstrap.Tooltip.getOrCreateInstance(buttonEl);
    } else {
        buttonEl.textContent = text;
    }
    buttonEl.dataset.actionName = name;
    buttonEl.classList.add("btn", "btn-sm", ...className?.split(" "));
    return buttonEl;
};

/**
 * Creates a div element for button actions with multiple action buttons.
 * @param {Object[]} buttons - Array of objects representing action buttons.
 * @returns {HTMLDivElement} - The div element containing the action buttons.
 */
const renderTdAction = (buttons = []) => {
    const actionEl = document.createElement("div");
    actionEl.className = "d-flex gap-1";

    buttons.forEach((button) => {
        actionEl.append(createButtonAction(button));
    });

    return actionEl;
};
```

```js
export { DataTable, renderTdAction };
```

## Use

resources\js\views\dashboard\tag\index.view.js

```js
import { DataTable, renderTdAction } from "@/plugins/dataTable";
```

```js
const tableTag = new DataTable(tableTagEl, {
   columns: [
       //...,
       {
           title: "Action",
           data: null,
           render: () => {
               return renderTdAction([
                   {
                       text: "Edit",
                       name: "buttonEdit",
                       icon: "bi-pencil-square",
                       className: "btn-primary",
                   },
                   {
                       text: "Hapus",
                       name: "buttonDelete",
                       icon: "bi-trash",
                       className: "btn-danger",
                   },
               ]);
           },
       },
   ],
});
```

## Ref

- [Document: createElement() method - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement)

- [HTML DOM Document createElement() Method](https://www.w3schools.com/jsref/met_document_createelement.asp)

- https://www.javascripttutorial.net/javascript-dom/javascript-createelement/
