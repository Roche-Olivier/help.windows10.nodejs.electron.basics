### [![Index](https://github.com/Roche-Olivier/help.windows10.nodejs.electron.basics/blob/master/_content/_images/home.png "Index") Index](https://github.com/Roche-Olivier/help.windows10.nodejs.electron.basics)

## Setup a logical folder structure

This part is how i like to set up my directory structure for an application.

We would not like to have hundreds of files in the root directory, so lets create a directory structure where we can group things together.

The html is the first glaring item we would like to get into a separate directory. This represents the client side of things.

Create a `src` directory under your application directory. Then create a sub directory under `src` called `content`.

We have created an area for all the pages and their content.

Now lets create all the parts within the `content` folder.
Create the following folders under `content`  : `css`, `images`, `js`, `pages`


All ready to go , all that we need to do now is add the `index.html` to the `pages` directory.To do this cut the `index.html` from the main application directory and paste it into the `pages` sub directory.


We have effectively broken our application now , and need to correct the folder structure.
When we work with the folder structure we need a new module of node called `path`.
Open your command prompt to the main application directory and type the following command:

`> npm install path`

This will install path under your `node-modules` and we can use it in the code.
Note:
Your package.json file has been updated to look like this:
``` 
 "dependencies": {
    "electron": "^5.0.4",
    "path": "^0.12.7"
  }
```

Open you `main.js` file and add the following to the top:
``` 
const path = require('path')
```
We need to change the path of the window that needs to be loaded , and this gets done by changing the `win.loadFile` command.
``` 
win.loadFile(path.join(__dirname + '/src/content/pages/index.html'))
```

Change the event listener to be able to call a function in another directory 
``` 
app.on('ready', () => {
  createWindow()
})
```
Your main.js file should look like this now 
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
|            +-- index.html
|   +-- main.js
|   +-- package-lock.json
|   +-- package.json
|   +-- README.md
```

All set your application now has its pages in a separate directory to easily discern the different functions of the application.

Save all the files and open your command prompt in your application folder.
Run the following command :

`> npm start `

Your application will start and open an electron window that looks like this:

![applicaiton_image](https://github.com/Roche-Olivier/help.windows10.nodejs.electron.basics/blob/master/_content/_images/screen/ex1_electron_screen.png "Application screen")

![Examples and lessons](https://github.com/Roche-Olivier/help.windows10.nodejs.electron.basics/blob/master/_content/_images/footer.png "Examples and lessons")



