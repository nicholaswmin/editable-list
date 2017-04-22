[![Build Status](https://travis-ci.org/nicholaswmin/editable-list.svg?branch=master)](https://travis-ci.org/nicholaswmin/editable-list)

# editable-list

> CRUD list in [Polymer 2.x][1]

<div style="text-align:center"><img src="http://i.imgur.com/p1fm4eE.png"/></div>


## The markup

There's 2 elements which you need to use:

- `<editable-list>`, the element itself which contains headers & rows
- `<editable-item>`, the repeated row

For example, the following markup creates the list displayed above:

```html
<link rel="import" href="bower_components/editable-list.html">
<link rel="import" href="bower_components/editable-item.html">


<style is="custom-style">
  /* You can style headers and/or row content with regular CSS */

  editable-item {
    display: flex;
    align-items: center;
  }

  .item {
    display: inline-block;
    width: 25%;
    padding: 0.35em;
  }

  .attachment-btn {
    color: #FF9800;
  }
</style>
<editable-list>
  <header slot="header">Country</header>
  <header slot="header">City</header>
  <header slot="header">Verified</header>
  <template>
    <editable-item item="{{item}}">
      <paper-input class="item" value="{{item.country}}" no-label-float></paper-input>
      <paper-input class="item" value="{{item.city}}" no-label-float></paper-input>
      <paper-checkbox class="item" checked="{{item.verified}}"></paper-checkbox>
      <paper-icon-button
        slot="actions"
        class="attachment-btn"
        icon="attachment"
        on-click="aFuncInHostElement">
      </paper-icon-button>
    </editable-item>
  </template>
</editable-list>

<!-- Where `aFuncInHostElement() can be a function in the host element that
contains this <editable-list>` -->
```


## View this element

```bash
$ npm install -g polymer-cli@next
$ bower install
$ polymer serve
```


## Running tests

```bash
$ npm install && npm install -g web-component-tester
$ polymer test

# Or run both `$ polymer test && polymer lint`
$ npm test
```


## The good stuff

It's flexible. You can easily change the DOM of each row, apply CSS to it
from the containing element & call functions of the containing element.

Nevertheless, the Shadow DOM encapsulation principles apply as usual.


## Passing Data

Accepts an object as `data` that looks like this:

> Note that the supplied `data` is 2-way data bound. Inline editing of rows
will reflect the changes to the supplied object and the observer firings will
propagate as usual to the host element.

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

[1]:https://www.polymer-project.org/2.0/docs/about_20


## License

Read "LICENSE.md" file in root directory
