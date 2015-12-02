# postcss-namespace

[![npm version](https://badge.fury.io/js/postcss-namespace.svg)](https://badge.fury.io/js/postcss-namespace)

[PostCSS](https://github.com/postcss/postcss) plugin that prefix a namespace to a selector

## Install

```
npm i postcss-namespace

# if still
npm i postcss
```

## Usage

Write `@namespace` atrule to your css file.
(e.g. input.css)
```css
.outside {}

@namespace block;

.box {}
.inner {}

.inner .exists {}
.inner .new {}
.inner .exists,
.inner .outside {}

.exists {}

@namespace ;

.box {}
.inner {}

@namespace block2;

.box {}
[class*="box"] {}
.inner {}

```

Use this plugin in PostCSS
(e.g.)
```javascript
var fs = require('fs');
var postcss = require('postcss');
var namespace = require('postcss-namespace');
var css = fs.readFileSync('input.css', 'utf8');

var output = postcss()
  .use(namespace({token: '__'}))
  .process(css)
  .css;

console.log(output);
```

Will get `output` like following CSS

```css
.outside {}

.block__box {}
.block__inner {}

.block__inner .block__exists {}
.block__inner .new {}
.block__inner .block__exists,
.block__inner .outside {}

.block__exists {}

.box {}
.inner {}

.block2__box {}
[class*="box"] {}
.block2__inner {}
```

## Options

- `token`  
  Token for consolidate(e.g.) `namespace({token: '__'})`  
  By default, it is `-`

## Run to example

**1** Close this

```
git clone git@github.com:totora0155/postcss-namespace.git
```

**2** Change directory
```
cd postcss-namespace
```

**3** Install modules
```
npm install
```

**4** Run to script
```
npm run example
```
