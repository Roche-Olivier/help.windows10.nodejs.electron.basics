[![Index](https://github.com/Roche-Olivier/help.windows10.nodejs.electron.basics/blob/master/_content/_images/footer.png "Table fo contents")](https://github.com/Roche-Olivier/help.windows10.nodejs.electron.basics)

## Hello world

This was extracted from : https://electronjs.org/docs/tutorial/first-app

Create an application folder.

Change your directory to the newly created folder.
Initialize the application with the following command:

`> npm init`

Complete all the relevant fields , and make the entry point 'main.js'
Now that the application is initialized , you can start to add the packages we are going to use.

This is an electron example so we would have to install electron.
Use the following command in the directory you are in.

`> npm install electron`

Electron gets installed into your application and you now have a `node_modules` folder in your application.
Remember to omit this from check-ins.

> Electron apps are developed in JavaScript using the same principles and methods found in Node.js development. All APIs and features found in Electron are accessible through the `electron` module, which can be required like any other Node.js module:


Create a file with the name `main.js` in your application root folder.

Start the application by adding the electron module to the `main.js` file

`const electron = require('electron')`

> The electron module exposes features in namespaces. As examples, the lifecycle of the application is managed through electron.app, windows can be created using the electron.BrowserWindow class. A simple main.js file might wait for the application to be ready and open a window:

Below is the simple example to just open a window.
Edit your `main.js` file to look like this:

``` 
 const { app, BrowserWindow } = require('electron')

 function createWindow () {
   // Create the browser window.
   let win = new BrowserWindow({
     width: 800,
     height: 600,
     webPreferences: {
       nodeIntegration: true
     }
   })

   // and load the index.html of the app.
   win.loadFile('index.html')
 }

app.on('ready', createWindow)
```

Create a new file called `index.html` in the application root folder.

Edit your `index.html` file to look like this:

``` 
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

Create a `README.md` file to detail you application.
Read-me files are normally done in mark down

For example:
``` 
# Electron example 1  - A very basic application

[Consult the wiki for more info.](https://github.com/Roche-Olivier/Examples/wiki/Electron-example-1)

```


Your folder structure should look like this now:
``` 
+-- application_folder
|   +-- node_modules
|   +-- index.html
|   +-- main.js
|   +-- package-lock.json
|   +-- README.md
```

Edit your `package.json` file , and add the `start` command to the `scripts` item for example:
``` 
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "electron ."
  },
```

Save all the files and open your command prompt in your application folder.
Run the following command :

`> npm start `

Your application will start and open an electron window that looks like this:

![applicaiton_image](https://github.com/Roche-Olivier/help.windows10.nodejs.electron.basics/blob/master/_content/_images/screen/ex1_electron_screen.png "Application screen")

[![Index](https://github.com/Roche-Olivier/help.windows10.nodejs.electron.basics/blob/master/_content/_images/footer.png "Table fo contents")](https://github.com/Roche-Olivier/help.windows10.nodejs.electron.basics)



