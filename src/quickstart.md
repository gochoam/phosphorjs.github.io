Getting Started
---------------

For developers familiar with Javascript tools.

Phosphor provides flexible classes to easily produce a desktop-like experience.
As introduction to PhosphorJS the following example prints the popular "Hello World"
message inside two resizable panels.

PhosphorJS is a set of javascript libraries, as such it can be used with any
framework. There is no "correct" way of using Phosphor. This example uses
typescript, the content is later bundled for the browser with webpack.

This is the content of `index.ts`:

```typescript

'use strict';

import {
  Widget
} from 'phosphor-widget';

import {
  DockPanel
} from 'phosphor-dockpanel';

let w1 = new Widget();
w1.addClass('content');
w1.node.innerHTML = "Hello";

let w2 = new Widget();
w2.addClass('content');
w2.node.innerHTML = "World";

let panel = new DockPanel();
panel.insertLeft(w1);
panel.insertRight(w2);

window.onload = () => { panel.attach(document.body); };
```

Use `npm` to Install the required packages to build your bundle with `webpack`:

```
npm install -g webpack typescript

npm install --save phosphor-dockpanel phosphor-widget css-loader style-loader ts-loader
```

The corresponding configuration file `webpack.config.json` looks like this:

```json
module.exports = {
  entry: './index.ts',
  output: {
    filename: './bundle.js'
  },
  resolve: {
    extensions: ['', '.ts', '.js']
  },
  bail: true,
  module: {
    loaders: [
      { test: /\.ts$/, loader: 'ts-loader' },
      { test: /\.css$/, loader: 'style-loader!css-loader' },
    ]
  }
}
```

At this point running `webpack` inside the current working directory will
produce `bundle.js`, this file can then be inserted in your `index.html` file:

```html
<!DOCTYPE html>
<html>
<head>
  <link href="index.css" rel="stylesheet">

  <script type="text/javascript" src="bundle.js"></script>
</head>
<body>
</body>
</html>
```

The HTML file also imports a style sheet, otherwise when the page is viewed in
the browser there will be a blank page only. This simple css files sets the
background color, the font size and the initial minimal size of the panels:

```css
.content {
  border: 1px solid black;
  min-width: 200px;
  min-height: 100px;
  font-size: large;
  background: #F3F3F3;
}
```
