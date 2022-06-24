# `mail3-me-button`

`mail3-me-button`  provides a simple way to interact with [Mail3 App](https://app.mail3.me).

## Usage

`mail3-me-button` is a [Web Component](https://developer.mozilla.org/en-US/docs/Web/Web_Components), Just like an HTML element, `mail3-me-button` has some built-in attributes:

* `filter(string)`: `filter` can pass in an email address, If an address is provided, `mail3-me-button` displays the number of unread messages between this address and the currently logged-in mailbox in Mail3 app, otherwise it displays the number of all unread messages.
* `lite(boolean)`: in lite mode, `mail3-me-button` will be displayed as a circular Icon without text.
* `variant(string)`: Some default style set for `mail3-me-button`, optionally one of `solid`, `outline`, `ghost`, default is `solid`
* `icon_type(string)`: Icon type for Mail3 Icon, optionally one of `black`, `white`, `light`, `solid`, default is `solid`
* `icon_style(string)`: CSS style for Mail3 Icon

In addition to the above built-in attributes, `mail3-me-button` also supports passing in all the attributes of [the anchor element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a), such as `style`, `target`, etc.

### HTML

[Live demo](https://stackblitz.com/edit/mail3-me?file=index.html)

After adding the `mail3-me-button` script, you can use it like an HTML element.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Mail3 Me Button Demo</title>
    <meta charset="UTF-8" />
  </head>

  <body>
    <!-- 3KiB gziped with public cdn, it is recommended that self-hosted this script -->
    <script src="https://unpkg.com/@mail3/mail3-me"></script>
    <mail3-me filter="only mails from this address will show notification" />
  </body>
</html>
```

### React

[Live demo](https://stackblitz.com/edit/mail3-me-react?file=src%2Fstyle.css,src%2FApp.js,src%2Findex.js)

Install `mail3-me-button`:

```bash
$ npm i @mail3/mail3-me
# or yarn
$ yarn add @mail3/mail3-me
```

Import the dependency in the entry file of your application:

```js
// app.js
// only 3KiB gziped
import '@mail3/mail3-me'
```

Use `mail3-me-button` like an HTML Element:

```jsx
<App>
  <Navbar />
  <mail3-me filter="mail3.eth@mail3.me" />
</App>
```

#### Caveats

The `style` attribute is replaced by the `css` attribute, and all custom style attribute should pass in a `string` type instead of `Object`.

```jsx
<App>
  <Navbar />
  <mail3-me css="width: 200px;" icon_style="width: 20px;" />
</App>
```
