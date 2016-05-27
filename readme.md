# Electron
### Build cross platform desktop apps with JavaScript, HTML, and CSS

Electron enables you to create desktop applications with pure JavaScript by providing a runtime with rich native (operating system) APIs. You could see it as a variant of the Node.js runtime that is focused on desktop applications instead of web servers.

This doesn't mean Electron is a JavaScript binding to graphical user interface (GUI) libraries. Instead, Electron uses web pages as its GUI, so you could also see it as a minimal Chromium browser, controlled by JavaScript.

## Structure
Generally, an Electron app is structured like this:

```text
your-app/
├── package.json
├── main.js
└── index.html
```

## Write your First Electron App
Create NodeJS app and install Electron
```bash
npm init
npm install electron
npm install electron-prebuilt
```

Replace 'Script' with this in the package.json file

```json
"scripts": {
    "start": "electron .",
    "build": "electron-packager ./ --platform=win32 --arch=all --version=1.2.0 --overwrite"
  },
```

Create app.js and index.html file
```javascript
const electron = require('electron');
const {app} = electron;
const {BrowserWindow} = electron;

let win;

function createWindow() {
  win = new BrowserWindow({width: 800, height: 600});
  win.loadURL(`file://${__dirname}/index.html`);
  win.on('closed', () => {
    win = null;
  });
}

app.on('ready', createWindow);

app.on('window-all-closed', () => {
  if (process.platform !== 'darwin') {
    app.quit();
  }
});

app.on('activate', () => {
  if (win === null) {
    createWindow();
  }
});
```

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>Hello World!</title>
  </head>
  <body>
    <h1>Hello World!</h1>
    We are using node <script>document.write(process.versions.node)</script>,
    Chrome <script>document.write(process.versions.chrome)</script>,
    and Electron <script>document.write(process.versions.electron)</script>.
  </body>
</html>
```

### Run your app
```bash
npm run start
```

### Build your app
```bash
npm run build
```
