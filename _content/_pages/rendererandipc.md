[![Index](https://github.com/Roche-Olivier/help.windows10.nodejs.electron.basics/blob/master/_content/_images/footer.png "Table fo contents")](https://github.com/Roche-Olivier/help.windows10.nodejs.electron.basics)

## Renderer and IPC events

Firstly we need to create directory `renderer` with the following path `src > content > renderer`.



Create a file called `app_main_renderer.js` in the `renderer` directory.

This file will be used in the `app_main.html` page. 

Match the name of the renderer with the name of the page.


Your `app_main_renderer.js` file will look like this when we are finished. 
```
const { ipcRenderer } = require('electron')
console.log("renderer loaded")
document.addEventListener('readystatechange', event => {
    if (event.target.readyState === "interactive") {
        console.log("same as  document.addEventListener("DOMContentLoaded"...") 
        console.log("same as  jQuery.ready") 
        console.log("All HTML DOM elements are accessible");
    }
    if (event.target.readyState === "complete") {
        console.log("Now external resources are loaded too, like css,src etc... ");
        console.log("The current user is :" + process.env.USER)
        ipcRenderer.send('opened_main_page', 'User opened page, all content loaded.')
    }
});
```

Lets see how its broken down

The ipcRenderer process is needed to speak to the ipcMain process, so we add that to the file.
The console.log is just to demonstrate what happens at which part of the calls.
```
const { ipcRenderer } = require('electron')
console.log("renderer loaded")
```


This part is an event listener to check when the page is loaded. The method catches both the DOM ready and PAGE ready events.
```
const { ipcRenderer } = require('electron')
console.log("renderer loaded")
document.addEventListener('readystatechange', event => {
    if (event.target.readyState === "interactive") {
        ...
    }
    if (event.target.readyState === "complete") {
        ...
    }
});
```

To fire an event to the ipcMain process you call the `ipcRenderer.send` command.
The first parameter is the event name and the second part is the data
```
ipcRenderer.send('opened_main_page', 'User opened page, all content loaded.')
```


Add the following script tags in your body of your app_main.html file
```
    <script>
        require('../renderer/app_main_renderer.js')
    </script>
```

Your html page will now fire an event to the ipcMain process as soon as everything is loaded.

BUT WAIT , What ipcMain , we dont have anything like that. In example 3 we added a file called ipc_main.js
Add the following code the the ipc_main.js file. This will call the sender back.
```
const { ipcMain } = require('electron')
ipcMain.on('opened_main_page',(event, arg)=>{
    console.log(arg)
    event.reply('opened_main_page_reply', 'Start to open the page, all content is loaded and the log of the opening is 
    caught.')
})
```

Update the main.js file to import the ipc_main.js file when loading the application
```
const start = require('./src/ipc/_start')
const ipc_main = require('./src/ipc/ipc_main')
```


Update the java script on the `app_main.html` file to handle the response from the `ipcMain` process

```
<script>
  const { ipcRenderer } = require('electron')
  ipcRenderer.on('opened_main_page_reply', (event, arg) => {

    console.log(arg)
    //everything is loaded start the page load

  })
</script>
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
|         +-- renderer
|            +-- app_main_renderer.js
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

![applicaiton_image](https://github.com/Roche-Olivier/help.windows10.nodejs.electron.basics/blob/master/_content/_images/screen/ex1_electron_screen.png "Application screen")

[![Index](https://github.com/Roche-Olivier/help.windows10.nodejs.electron.basics/blob/master/_content/_images/footer.png "Table fo contents")](https://github.com/Roche-Olivier/help.windows10.nodejs.electron.basics)




