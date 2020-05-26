### [![Index](https://github.com/Roche-Olivier/help.windows10.nodejs.electron.basics/blob/master/_content/_images/home.png "Index") Index](https://github.com/Roche-Olivier/help.windows10.nodejs.electron.basics)

## Splitting the main file


This is how i like to split my `main.js` file to get more functionality out of the parts , and the split them into their own functional groups.

We already have the `src` directory under the main application directory

Create a new directory called `ipc` under the `src` directory.We will break down the `main.js` file into 3 separate files and create a directory for each type of functionality


Under the `ipc` directory create 3 new files called `_start.js`,  `ipc_main.js` and `ipc_windows.js`
The structure is now created , and we can start. where else but at the start and for that we go to the _start.js file

Cut all the contents of the `main.js` file and copy it into the `_start.js` file. 
On the `main.js` file make a reference to the start file like this const `start = require('./src/ipc/_start')`
This will tell the app to use the start file.
So your `main.js` file should look like this now:

``` 
const start = require('./src/ipc/_start')
```

and your _start.js like this :

``` 
const { app, BrowserWindow } = require('electron')
const path = require('path')

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
  win.loadFile(path.join(__dirname + '/src/content/pages/index.html'))
}

app.on('ready', () => {
  createWindow()
})

```
The next thing we need to do is to take the window creation out of the start and into a window manager file to have all the window creation events in one place.


Cut the `createWindow` function from the `_start.js` file and paste it into the `ipc_windows.js` file.
Change the name of your `index.html` file to `app_main.html`
Open your `ipc_window.js` file and add the following lines to the top.
``` 
const {  BrowserWindow } = require('electron')
const path = require('path')
``` 
We have moved the functionality , so we need to add the electron objects to this new file.
The path has also changed relative to the file location.
Change the function to be exportable.
Your `ipc_window.js` file should now look like this:
``` 
const {  BrowserWindow } = require('electron')
const path = require('path')
exports._windows = {
    load_main_window: function () {
        // Create the browser window.
        let win = new BrowserWindow({
            width: 800,
            height: 600,
            webPreferences: {
                nodeIntegration: true
            }
        })
        // and load the index.html of the app.
        win.loadFile(path.join(__dirname + '../../content/pages/app_main.html'))
    }
}
``` 
Lets add a `window-all-closed` event to the start so that the application will end if all the windows are closed.
Add the following code to your `_start.js` file
``` 
// Quit when all windows are closed.
app.on('window-all-closed', () => {
    // On macOS it is common for applications and their menu bar
    // to stay active until the user quits explicitly with Cmd + Q
    if (process.platform !== 'darwin') {
        app.quit()
    }
})
```
Next thing we need to do is change the call method to create windows.
The part `createWindow()` can now be changed to refer to the method we created.
Declare the ipcwindows object in your `_start.js` file
``` 
var ipcwindows = require('./ipc_windows')
```
Now you can change the code to call the method in that file in your application.
``` 
ipcwindows._windows.load_main_window()
```

Your _start.js file should look like this now:
``` 
const { app } = require('electron')

var ipcwindows = require('./ipc_windows')

app.on('ready', () => {
    ipcwindows._windows.load_main_window()
})

// Quit when all windows are closed.
app.on('window-all-closed', () => {
    // On macOS it is common for applications and their menu bar
    // to stay active until the user quits explicitly with Cmd + Q
    if (process.platform !== 'darwin') {
        app.quit()
    }
})
```

Your folder structure should look like this now:
``` 
+-- application_folder
|   +-- node_modules
|   +-- src
|      +-- content
|         +-- css
|         +-- images
|         +-- js
|         +-- pages
|            +-- app_main.html
|      +-- ipc
|         +-- _start.js
|         +-- ipc_main.js
|         +-- ipc_windows.js
|   +-- main.js
|   +-- package-lock.json
|   +-- package.json
|   +-- README.md
```


Save all the files and open your command prompt in your application folder.
Run the following command :

`> npm start `

Your application will start and open an electron window that looks like this:

![applicaiton_image](https://github.com/Roche-Olivier/Examples/blob/master/Images/ex1_electron_screen.png "Application screen")


![Examples and lessons](https://github.com/Roche-Olivier/help.windows10.nodejs.electron.basics/blob/master/_content/_images/footer.png "Examples and lessons")



