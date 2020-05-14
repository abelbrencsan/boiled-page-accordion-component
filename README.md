# Boiled Page accordion component

Accordion SCSS component for Boiled Page frontend framework. It is intended to create collapsible accordions.

## Install

Place `_accordion.scss` file to `/assets/css/components` directory, and add its path to components block in `assets/css/app.scss` file. You will also need to add accordion script to make it working properly.

- Accordion script: <https://www.github.com/abelbrencsan/boiled-page-accordion-script>

## Usage

### Classes

Class name | Description | Example
---------- | ----------- | -------
`accordion` | Applies an accordion. | `<ul class="accordion"></ul>`

### Examples

#### Example 1

The following example shows a simple collapsible accordion. `data-accordion` attributes are used for accordion script.

```html
<ul class="accordion" data-accordion>
  <li data-accordion-item>
    <button type="button" data-accordion-item-trigger>Accordion trigger 1</button>
    <div data-accordion-item-element>
      <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
    </div>
  </li>
  <li data-accordion-item>
    <button type="button" data-accordion-item-trigger>Accordion trigger 2</button>
    <div data-accordion-item-element>
      <p>Vestibulum sit amet bibendum metus, dapibus dictum tellus.</p>
    </div>
  </li>
  <li data-accordion-item>
    <button type="button" data-accordion-item-trigger>Accordion trigger 3</button>
    <div data-accordion-item-element>
      <p>Fusce neque arcu, semper eu lacus sed, scelerisque accumsan ipsum.</p>
    </div>
  </li>
</ul>
```

Add `accordions` property to `app` object in `assets/js/app.js`.

```js
accordions: []
```

The following JavaScript initalizes elements with `data-accordion` attribute as accordions.

```js
// Initialize accordions
var accordionElems = document.querySelectorAll('[data-accordion]');
for (var i = 0; i < accordionElems.length; i++) {
  app.accordions[i] = new Accordion({
    items: Array.prototype.map.call(accordionElems[i].querySelectorAll('[data-accordion-item]'), function(obj) {
      return {
        trigger: obj.querySelector('[data-accordion-item-trigger]'),
        element: obj.querySelector('[data-accordion-item-element]')
      };
    }),
  });
  app.accordions[i].init();
}
```

Place the following code inside the `onBreakpointChange` function in `assets/js/app.js` to recalculate maximum height of opened accordion item's element when breakpoint changes.

```js
// Recalculate maximum height of opened accordion item's element
for (var i = 0; i < app.accordions.length; i++) {
  app.accordions[i].recalcHeight();
}
```
