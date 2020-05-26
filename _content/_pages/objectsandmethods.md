### [![Index](https://github.com/Roche-Olivier/help.windows10.nodejs.electron.basics/blob/master/_content/_images/home.png "Index") Index](https://github.com/Roche-Olivier/help.windows10.nodejs.electron.basics)

## Objects and methods

Where and how you create your objects and methods is up to you , but i like to create my objects and methods on the following way.

My global values i like to put in the `process.env.var` , that way you can access it anywhere.
This should be a global value as it runs in the main process, and not on the windows, we can add window `process.env.var` as well but that will only be applicable on that window ( or process that kicked off )


Create a folder called `scripts` under your main application directory. This is where we will put all the application scripts into, things that all windows will use.
Then create a folder under the `src > content > js > document_models` this will be where all the page scripts will reside of the doc model.


Lets see how this works.
Create a file called `_general.js` under the `src > content > js > document_models` directory.
We can now put all the general things in here , things that all the window document models will use.


Create a method in the `_general.js` file that will alert the user the page has loaded.
```
exports.alerts = {
    loaded: function () {
        alert("loaded")
    }
}
```

Now lets hook this new method up on the page. Open your `app_main.html` page and in the scripts part add the reference to the general file like this :
```
const _general = require('../js/document_models/_general')
```
Now that you have added the reference , you can add the call to the script we did in example 4, like this
```
  ipcRenderer.on('opened_main_page_reply', (event, arg) => {

    console.log(arg)
    _general.alerts.loaded()
    //everything is loaded start the page load

  })
```

Your scripts part of the `app_main.html` file will now look like this 

```

<script>
  require('../renderer/app_main_renderer.js')
</script>

<script>
  const { ipcRenderer } = require('electron')
  const _general = require('../js/document_models/_general')

  ipcRenderer.on('opened_main_page_reply', (event, arg) => {

    console.log(arg)
    _general.alerts.loaded()
    //everything is loaded start the page load

  })
</script>
```

Lets move the scripts together to only have one script section on the page.
```
<script>
  require('../renderer/app_main_renderer.js')
  const { ipcRenderer } = require('electron')
  const _general = require('../js/document_models/_general')
  ipcRenderer.on('opened_main_page_reply', (event, arg) => {
    console.log(arg)
    _general.alerts.loaded()
  })
</script>
```

Your folder structure should look like this now:
``` 
+-- application_folder
|   +-- node_modules
|   +-- scripts
|   +-- src
|      +-- content
|         +-- css
|         +-- images
|         +-- js
|            +-- document_models
|               +-- _general.js
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

![applicaiton_image](https://github.com/Roche-Olivier/Examples/blob/master/Images/ex1_electron_screen.png "Application screen")


![Examples and lessons](https://github.com/Roche-Olivier/help.windows10.nodejs.electron.basics/blob/master/_content/_images/footer.png "Examples and lessons")



