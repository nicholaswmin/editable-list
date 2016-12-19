# editable-list

> A Light-DOM enabled editable list in [Polymer 2.0][1]

> Please refrain from using this in production code.
> It's built on top of Polymer 2.0 which doesn't have a stable API yet as
it's still in development. Futhermore there's no unit tests or real documentation

<div style="text-align:center"><img src="http://i.imgur.com/p1fm4eE.png"/></div>

### The markup

The intention was to abstract away the repeater (`dom-repeat`), the add/delete
buttons and some list-related general CSS whilst still allowing custom markup,
binding to external methods & styling of the custom markup (via the Light-DOM).

While there are some samples floating around that make use of the Templatizer
to achieve the above, there's no samples that use the `dom-repeat` element
already provided by Polymer therefore they usually re-implement a lot of the
functionality already present in `dom-repeat`.

The following markup creates the list displayed above.

```html
<style is="custom-style">
  .attachement-btn {
    color: #FF9800;
  }
</style>

<editable-list data="{{data}}">
  <!-- Headers -->
  <div slot="header" class="flex-2 field-container">Country</div>
  <div slot="header" class="flex-2 field-container">City</div>
  <div slot="header" class="flex field-container">Verified</div>
  <!-- /Headers-->
  <!-- Row Markup, usage is identical to `dom-repeat`-->
  <template>
    <editable-item class="layout horizontal center list-item" item="[[item]]">
      <paper-input class="flex-2" value="{{item.country}}" no-label-float></paper-input>
      <paper-input class="flex-2" value="{{item.city}}" no-label-float></paper-input>
      <paper-checkbox class="flex" value="{{item.verified}}"></paper-checkbox>
      <!-- Add row-specific actions. You can bind to methods as usual -->
      <paper-icon-button slot="row-actions" icon="attachment"></paper-icon-button>
    </editable-item>
  </template>
  <!-- /Row markup-->
</editable-list>
```


## The good stuff

  - Based on Polymer 2.0
  - Piggybacks on `dom-repeat`. Doesn't reinvent the wheel.
  - Headers/Rows can span 1,2,3,4,5 or whatever number of columns you want.
  Just use the `iron-flex-layout` classes.
  - Add your own row-specific buttons using `slot="row-actions"`
  - Style your item/actions markup externally.
  - Bind your markup to external methods

Note that the headers & rows are appended to the Light DOM therefore you can
bind to methods outside of `editable-list`. The same applies for styling.

The Shadow-DOM encapsulation-principle applies as usual for everything else.

## The not-so-good stuff

- It's based on Polymer 2.0 which is still in preview and it's API is subject
to change.
- There's no docs or tests.


*Don't use this in production code, yet*


## Usage

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


## Docs? Tests? - where are they?

I'm waiting for the Polymer Team to put some Polymer 2.0 seed element templates
in the Polymer CLI. You can track the Issue [here][2]

Until then, this is just an experiment.

## LICENSE

> The MIT License (MIT)

> Copyright (c) 2016 Nicholas Kyriakides

> Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

> The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

> THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

[1]:https://www.polymer-project.org/2.0/docs/about_20
[2]:https://github.com/Polymer/polymer-cli/issues/443
