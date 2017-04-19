[![Build Status](https://travis-ci.org/nicholaswmin/editable-list.svg?branch=master)](https://travis-ci.org/nicholaswmin/editable-list)


# editable-list

> CRUD list in [Polymer 2.x][1]

<div style="text-align:center"><img src="http://i.imgur.com/p1fm4eE.png"/></div>

## The markup

The following markup creates the list displayed above.

```html
<style is="custom-style">
  .aligner {
    display: flex;
    align-items: center;
  }

  .item {
    display: block;
    float: left;
    width: 25%;
    padding: 0.35em;
  }

  .attachment-btn {
    color: #FF9800;
  }
</style>
<editable-list>
  <div slot="header" class="item">Country</div>
  <div slot="header" class="item">City</div>
  <div slot="header" class="item">Verified</div>
  <template>
    <editable-item class="aligner list-item" item="{{item}}">
      <paper-input class="item" value="{{item.country}}"></paper-input>
      <paper-input class="item" value="{{item.city}}"></paper-input>
      <paper-checkbox class="item" checked="{{item.verified}}"></paper-checkbox>
      <paper-icon-button
        slot="actions"
        class="attachment-btn"
        icon="attachment"
        on-click="auxButtonPressed">
      </paper-icon-button>
    </editable-item>
  </template>
</editable-list>
```


## The good stuff

  - Piggybacks on `dom-repeat`. Doesn't reinvent the wheel.
  - Add row-specific buttons using `slot="row-actions"`
  - Style items/actions markup externally.
  - Bind your markup to methods as usual

Note that the headers & rows are appended to the Light DOM therefore you can
bind to methods outside of `editable-list`. The same applies for styling.

The Shadow-DOM encapsulation-principle applies as usual for everything else.


## Passing Data

Accepts an object as `data` that looks like this:

> Note that the supplied `data` is 2-way data bound. Inline editing of rows
will reflect the changes to the supplied object and the observer firings will
propagate as usual.

```javascript
 data = {
   // Rows are added here.
   contents: [
      {
        id: 1, // Must be a unique identifier
        country: "United Kingdom",
        city: "London",
        verified: true
        // .. rest of props
      },
      {
        id: 2,
        prop1: "China",
        prop2: "Beijing",
        verified: false
      }
   ],
   /*
    * Deleted rows are accumulated here. Keep in mind that rows that weren't
    * initially provided in `contents` won't be pushed here.
    */
   deletedRows: []
 }
```

## Internals

The `template` of a row, see the `editable-item` parent, is picked up and
appended as the child of a `dom-repeat` inside the element.

This results internally to this:

```html
<dom-repeat items="{{data.contents}}">
  <template>
    <!-- Row markup defined in the Light DOM -->
  </template>
</dom-repeat>
```

The completed `dom-repeat` structure is then appended in the element's Light DOM,
thus allowing
direct styling and method binding from within the element that actually contains
the `editable-list`.

Technically speaking you could fork this element and use an `iron-list` in the
place of the `dom-repeat` - which is more efficient than the dom-repeat. At the
time of building this `iron-list 2.0` wasn't quite ready yet and there were
some problems with event handling (which is needed when deleting rows).

## View this element

```bash
$ npm install -g polymer-cli@next
$ npm install
$ bower install
$ polymer serve
```

## Running tests

```bash
$ npm install -g web-component-tester
$ polymer test

# Or run both `$ polymer test && polymer lint`
$ npm test
```

## License

> The MIT License (MIT)

> Copyright (c) 2017 Nicholas Kyriakides

> Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

> The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

> THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

[1]:https://www.polymer-project.org/2.0/docs/about_20
