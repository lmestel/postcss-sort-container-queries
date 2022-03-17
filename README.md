# PostCSS Sort Container Queries

[PostCSS]:          https://github.com/postcss/postcss
[MIT]:              https://github.com/lmestel/postcss-sort-container-queries/blob/master/LICENSE
[official docs]:    https://github.com/postcss/postcss#usage

[PostCSS] plugin for combine and sort CSS container queries with **mobile first** or **desktop first** methods.

> **Combine** same container queries into one - is a unexpected side effect for this plugin 🧬

# Examples

### Mobile first sorting

```css
/* before */
@container size(max-width: 640px) {
  .head { color: #cfcfcf }
}
@container size(max-width: 768px) {
  .footer { color: #cfcfcf }
}
@container size(max-width: 640px) {
  .main { color: #cfcfcf }
}
@container size(min-width: 1280px) {
  .mobile-first { color: #cfcfcf }
}
@container size(min-width: 640px) {
  .mobile-first { color: #cfcfcf }
}
@container size(max-width: 640px) {
  .footer { color: #cfcfcf }
}

/* after */
@container size(min-width: 640px) {
  .mobile-first { color: #cfcfcf }
}
@container size(min-width: 1280px) {
  .mobile-first { color: #cfcfcf }
}
@container size(max-width: 768px) {
  .footer { color: #cfcfcf }
}
@container size(max-width: 640px) {
  .head { color: #cfcfcf }
  .main { color: #cfcfcf }
  .footer { color: #cfcfcf }
}
```

### Desktop first sorting

```css
/* before */
@container size(max-width: 640px) {
  .header { color: #cdcdcd }
}
@container size(min-width: 760px) {
  .desktop-first { color: #cdcdcd }
}
@container size(max-width: 640px) {
  .main { color: #cdcdcd }
}
@container size(min-width: 1280px) {
  .desktop-first { color: #cdcdcd }
}
@container size(max-width: 760px) {
  .footer { color: #cdcdcd }
}
@container size(max-width: 640px) {
  .footer { color: #cdcdcd }
}

/* after */
@container size(max-width: 760px) {
  .footer { color: #cdcdcd }
}
@container size(max-width: 640px) {
  .header { color: #cdcdcd }
  .main { color: #cdcdcd }
  .footer { color: #cdcdcd }
}
@container size(min-width: 760px) {
  .desktop-first { color: #cdcdcd }
}
@container size(min-width: 1280px) {
  .desktop-first { color: #cdcdcd }
}
```

## Getting Started

First thing's, install the module:

```
npm install postcss postcss-sort-container-queries --save-dev
```

## 🍳 Usage

Check you project for existed PostCSS config: `postcss.config.js`
in the project root, `"postcss"` section in `package.json`
or `postcss` in bundle config.

If you already use PostCSS, add the plugin to plugins list:

```diff
module.exports = {
  plugins: [
+   require('postcss-sort-container-queries')({
+     // sort: 'mobile-first' default value
+     sort: function(a, b) {
+        // custom sorting function
+     }
+   }),
    require('autoprefixer')
  ]
}
```

If you do not use PostCSS, add it according to [official docs]
and set this plugin in settings.

## 🍰 Options

> Sorting works based on [dutchenkoOleg/sort-css-media-queries](https://github.com/dutchenkoOleg/sort-css-media-queries) function.

### sort

This option support **string** or **function** values.

- `{string}` `'mobile-first'` - (default) mobile first sorting
- `{string}` `'desktop-first'` - desktop first sorting
- `{function}` your own sorting function

#### `'mobile-first'`

```js
postcss([
  sortContainerQueries({
    sort: 'mobile-first' // default
  })
]).process(css);
```

#### `'desktop-first'`

```js
postcss([
  sortContainerQueries({
    sort: 'desktop-first'
  })
]).process(css);
```

#### Custom sort function
```js
postcss([
  sortContainerQueries({
    function(a, b) {
      return a.localeCompare(b);
    }
  })
]).process(css);
```

In this example, all your container queries will sort by A-Z order.

This sorting function is directly passed to Array#sort() method of an array of all your container queries.

### Sort configuration

By this configuration you can control sorting behaviour.

```js
postcss([
  sortContainerQueries({
    configuration: {
      unitlessMqAlwaysFirst: true, // or false
    }
  })
]).process(css);
```

Or alternatively create a `sort-css-mq.config.json` file in the root of your project. Or add property `sortCssMQ: {}` in your `package.json`.

---

## License

[MIT]

## Other PostCSS plugins

- [`postcss-momentum-scrolling`](https://github.com/solversgroup/postcss-momentum-scrolling) - plugin for adding **momentum** style scrolling behavior (`-webkit-overflow-scrolling:touch`) for elements with overflow (scroll, auto) on iOS

## Thanks 💪

- Andrey Sitnik [@ai](https://github.com/ai)
- Jakub Caban [@Lustmored](https://github.com/Lustmored)
- Dmytro Symonov [@Kassaila](https://github.com/Kassaila)
- Kai Falkowski [@SassNinja](https://github.com/SassNinja)
- Олег Дутченко [@dutchenkoOleg](https://github.com/dutchenkoOleg)
