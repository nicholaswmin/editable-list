# editable-list

Uses just this markup:

```html
<editable-list data="{{data}}">
  <!-- Headers -->
  <div slot="header" class="flex-2 field-container">2-col wide header</div>
  <div slot="header" class="flex-2 field-container">2-col wide header</div>
  <div slot="header" class="flex field-container">1-col wide header</div>
  <!-- Repeated Contents, usage is identical to `dom-repeat`-->
  <template>
    <editable-item class="layout horizontal center list-item" item="{{item}}">
      <paper-input class="flex-2" value="{{item.prop1}}" no-label-float></paper-input>
      <paper-input class="flex-2" value="{{item.prop2}}" no-label-float></paper-input>
      <paper-checkbox class="flex field-container" value="{{item.prop3}}"></paper-checkbox>
      <!-- Add buttons on your row -->
      <span slot="row-actions">
        <paper-icon-button icon="attachment"></paper-icon-button>
      </span>
    </editable-item>
    <!-- /End of Repeated Contents-->
  </template>
</editable-list>
```


## The good stuff

  - Based on Polymer 2.0
  - Piggybacks on `dom-repeat`. Doesn't reinvent the wheel.
  - Use whatever markup you want for your items/headers.
  - Add your own buttons using `slot=actions`
  - Style your item/actions markup externally.
  - Bind your markup to external methods

## The not-so-good stuff

- It's based on Polymer 2.0 which is still experimental and it's API is subject
to change.
- There's no docs or tests.


*Don't use this in production code, yet*


## Usage

Accepts a data-bound object as `data` that looks like this:

```javascript
 data = {
   contents: [
      {
        id: 1, // Must be a unique identifier
        prop1: "Foo",
        prop2: 12,
        prop3: true
        // .. rest of your props
      },
      {
        id: 2
        prop1: "Baz",
        prop2: 28,
        prop3: false
        // .. rest of your props
      }
   ],
   deletedRows: [
    // accumulates ids of deleted rows. Rows that weren't initially provided
    // in `contents` won't be pushed here.
   ]
 }
```

## Why?

I needed a reusable editable list which allows me to declare stuff directly
in it's Light DOM without using the `Templatizer`.

The `dom-repeat` element that comes with Polymer is already well-thought out
and this is what is used internally to repeat the declared Light DOM.

## Docs? Tests? - where are they?

I'm waiting for the Polymer Team to put some Polymer 2.0 seed element templates
in the Polymer CLI.

Until then, this is just an experiment.
