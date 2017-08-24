# Getting most out of using namespaces

Namespaces are a feature in i18next internationalization framework which allows you to separate translations that get loaded into multiple files.

While in a smaller project it might be reasonable to just put everything in one file you might get at a point where you want to break translations into multiple files. Reasons might be:

* You start loosing the overview having more than 300 segments in a file
* Not every translation needs to be loaded on the first page, speed up load time

> We recommend you to create multiple smaller namespaces.

## Semantic reasons

Often you wish to separate some segments out because they belong together. We do this in most of our projects, eg.:

* **common.json** -&gt; Things that are reused everywhere, eg. Button labels 'save', 'cancel'
* **validation.json** -&gt; All validation texts
* **glossary.json** -&gt; Words we want to be reused consistent inside texts [sample usage](http://i18next.com/translate/nesting/)

## Technical / editoral reasons

More often you don't want to load all the translations upfront or at least reduce the amount loaded. This reason often goes hand in hand with the one translation file gets to large and you start loosing the overview scrolling through hundred of text fragments.

* namespace per view/page
* namespace per application section / feature set \(admin area, ...\)
* namespace per module which gets lazy loaded \(single page applications\)

## Configuration / Usage:

### locize / i18next

```js
locize.init({
  ns: ['common', 'moduleA', 'moduleB'],
  defaultNS: 'moduleA'
}, (err, t) => {
  locize.t('myKey'); // key in moduleA namespace (defined default)
  locize.t('common:myKey'); // key in common namespace
});

// load additional namespaces after initialization
locize.loadNamespaces('myNamespace', (err, t) => { /* ... */ });
```

There are advanced options like:

* calling t function with multiple namespaces to look a key up
* default fallback namespaces to lookup keys in

more details: [locize / i18next](http://i18next.com/translate/namespace/)

### locizify

```js
locizify.init({
  namespace: 'myNamespace'
  ns: ['common', 'myNamespace'] // -> add additional namespaces to load
});
```

You can access a different namespace by setting the attribute i18next-options:

```html
<div i18next-options='{"ns": "common"}'>
  <p>different namespace common is used</p>
  <p>all the way down</p>
</div>
```

Optionally you can set locizify to create a namespace per location/route.

```js
locizify.init({
  namespaceFromPath: true
});
```

more details: [locizify](https://github.com/locize/locizify#set-different-namespaces)

