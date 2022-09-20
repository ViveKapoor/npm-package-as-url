# Loading NPM package from URL

A day ago, I felt like learning ReactJS and like is the tradition, I started with "Hello World!" single page react app. After successfully building the "Hello World!" app, now I want to share my journey because there's an interesting thing I discoverend along the way...

Okay, so here are the summarized steps to display "Hello World!" using React ?

1. Install `npm` (we need this to install react packages)
```bash
sudo apt install nodejs npm
```
2. Init npm
```bash
npm init
```
3. Install `react` and `react-dom`
```bash
npm install react react-dom --save
```

### What is npm and what happens when we do `npm install` ?
npm is the package manager for the Node JavaScript platform. It puts modules in place so that node can find them, and manages dependency conflicts intelligently. It is extremely configurable to support a wide variety of use cases. Most commonly, it is used to publish, discover, install, and develop node programs.

`npm install` downloads a package and it's dependencies. `npm install` can be run with or without arguments. When run without arguments, npm install downloads dependencies defined in a `package.json` file and generates a `node_modules` folder with the installed modules.
All the required packages can only be used after we download and install them using `npm install`

### Pre-requites for using ReactJS
In order to use ReactJS, I had to install these two packages with npm – `react` and `react-dom`

### Do we really need to download, install and compile these packages?
I wondered, since npm doesn't allow making any changes to published packages, can't we use the precompiled packages directly without the need of downloading, installing and resolving dependencies everytime I build my project(app)?

Well, after some research I found [https://unpkg.com/](https://unpkg.com/) which does exactly the same. It provides precompiled npm packages(bundle) for quick use. The code folder which would have looked something like this with multiple required files
![folder_structure](https://raw.githubusercontent.com/ViveKapoor/npm-package-as-url/main/folder_structure.png) now looks this small and simple one file:

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

If we look at these two lines in the above snippet, that's where all magic goes...
```
<script src="https://unpkg.com/react@16.12.0/umd/react.development.js"></script>
<script src="https://unpkg.com/react-dom@16.12.0/umd/react-dom.development.js"></script>
```
This loads the required packages `react` and `react-dom` from [https://unpkg.com/](https://unpkg.com/) at load time. As the precompiled packages are very small in size(generally speaking) and the fact that unpkg delivers it via Cloudflare's global CDN which caches it and servers it from the nearest location from the user, this improves the load time for the user.

### Unpkg workflow
Unpkg uses CDNs (content delivery networks) because they allow static assets like images, JavaScript, and videos to be hosted physically close to end users as well as served with as fast as possible technology. unpkg is sponsored by Heroku where it is hosted, but that server is only actually used 5% of the time. The real power of a tool like unpkg is the fact that the files hosted at those URLs can be very heavily cached (npm doesn't allow published packages to be changed). So unpkg is also sponsored by Cloudflare which serves 95% of unpkg's traffic from the cache, making unpkg extremely fast.


### Challenges solved
Getting the precompiled packages from unpkg (or other similar service) helps to solve a few challenges like:
- Need for developers to re-compile pre-existing packages(bundle). This reduces developer's time and hence improves efficiency
- Faster load times for end users
- Quickly bootstrapping simple ReactJS applications
- Ease to update dependencies to latest available version of the package



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
