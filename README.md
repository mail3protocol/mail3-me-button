# `mail-me-button`

`mail-me-button`  provides a simple way to interact with [Mail3 App](https://app.mail3.me).

## Usage

`mail-me-button` is a [Web Component](https://developer.mozilla.org/en-US/docs/Web/Web_Components), Just like an HTML element, `mail-me-button` has some built-in attributes:

* `address(string)`: If this address is provided, `mail-me-button` displays the number of unread messages between this address and the currently logged in mailbox in Mail3 app, otherwise it displays the number of all unread messages.
* `lite(boolean)`: in lite mode, `mail-me-button` will be displayed as a circular Icon without text.
* `variant(string)`: Some default style set for `mail-me-button`, optionally one of `solid`, `outline`, `ghost`, default is `solid`
* `icon(string)`: style for Mail3 Icon, optionally one of `black`, `white`, `light`, `solid`, default is `solid`

In addition to the above built-in attributes, `mail-me-button` also supports passing in all the attributes of [the anchor element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a), such as `style`, `target`, etc.

### HTML

[Live demo](https://stackblitz.com/edit/js-s517fy?file=index.html)

After adding the `mail-me-button` script, you can use it like an HTML element.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Mail Me Button Demo</title>
    <meta charset="UTF-8" />
  </head>

  <body>
    <!-- 3KiB gziped with public cdn, it is recommended that self-hosted this script -->
    <script src="https://unpkg.com/@mail3/mail-me"></script>
    <mail-me address="your email address" />
  </body>
</html>
```

### React

[Live demo](https://stackblitz.com/edit/react-fyjn1z?file=src/App.js)

Install `mail-me-button`:

```bash
$ npm i @mail3/mail-me
# or yarn
$ yarn add @mail3/mail-me
```

Import the dependency in the entry file of your application:

```js
// app.js
// only 3KiB gziped
import '@mail3/mail-me'
```

Use `mail-me-button` like an HTML Element:

```jsx
<App>
  <Navbar />
  <mail-me address="mail3.eth@mail3.me" />
</App>
```
