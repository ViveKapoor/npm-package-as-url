# Loading NPM package from URL

Let's take an example that we want to build simple "Hello World!" react page.

If we go by native approach, we will install `react` and `react-dom` npm packages which will download and install both packages and related dependencies. But wait, before that we also need to install npm!

Installation and configuration can take a while...

Is there a faster way to do this ? yes!

[https://unpkg.com/](https://unpkg.com/) provides a way to dowload the npm packages from CDN and use them directly. No need to install npm, react, or react-dom separately. Here's an example:

```html
<body>
  <div id="root"></div>
  <script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
  <script type="text/javascript">
    const rootElement = document.getElementById('root')
    const element = React.createElement('div',  {
      className: 'container',
      children: 'Hello World!'
    });
    ReactDOM.render(element, rootElement)
  </script>
</body>
```
![hello_world.png](https://raw.githubusercontent.com/ViveKapoor/npm-package-as-url/3ac60e2395d43a32bb95fdbcceb422e59ba22434/hello_world.png)
```
<script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
<script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
```
This loads the required packages `react` and `react-dom` from CDN. Isn't it as simple as saying "Hello World!" ? :wink:

Caching npm packages is possible because npm does't allow packages with same version to be re-published. Any npm package can be used in same way by requesting package in the below format:
```
unpkg.com/:package@:version/:file
```
We can also get metadata and module information of a package by providing relevant query params. For example:
`?meta`
Return metadata about any file in a package as JSON (e.g./any/file?meta)
`?module`
Expands all “bare” import specifiers in JavaScript modules to unpkg URLs. This feature is very experimental

There are more ways to load packages based on latest tag, listing, and more. Please visit `https://unpkg.com/` for more information on unpkg.
