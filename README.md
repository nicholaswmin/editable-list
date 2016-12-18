# editable-list

> A Light-DOM enabled editable list in Polymer 2.0

> DO NOT use this in production code - this is a personal experiment

![img](http://i.imgur.com/d7Sxn9P.png)

Uses just this markup:

```html
<editable-list data="{{data}}">
  <!-- Headers -->
  <div slot="header" class="flex-2 field-container">Country</div>
  <div slot="header" class="flex-2 field-container">City</div>
  <div slot="header" class="flex field-container">Verified</div>
  <!-- Repeated Contents, usage is identical to `dom-repeat`-->
  <template>
    <editable-item class="layout horizontal center list-item" item="{{item}}">
      <paper-input class="flex-2" value="{{item.country}}" no-label-float></paper-input>
      <paper-input class="flex-2" value="{{item.city}}" no-label-float></paper-input>
      <paper-checkbox class="flex field-container" value="{{item.verified}}"></paper-checkbox>
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
   // Rows are added here.
   contents: [
      {
        id: 1, // Must be a unique identifier
        country: "United Kingdom",
        city: "London",
        verified: true
        // .. rest of your props
      },
      {
        id: 2
        prop1: "China",
        prop2: "Beijing",
        verified: false
      }
   ],
   /*
    * Deleted rows are accumulated here.
    *
    * @NOTE Rows that weren't initially provided
    * in `contents` won't be pushed here.
    */
   deletedRows: []
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

## LICENSE

> The MIT License (MIT)

> Copyright (c) 2016 Nicholas Kyriakides

> Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

> The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

> THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
