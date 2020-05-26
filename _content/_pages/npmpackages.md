### [![Index](https://github.com/Roche-Olivier/help.windows10.nodejs.electron.basics/blob/master/_content/_images/home.png "Index") Index](https://github.com/Roche-Olivier/help.windows10.nodejs.electron.basics)

## Adding NPM packages

There are hundreds of thousands of NPM packages available. Lets look at how you would get the username from the pc the application is running on.

The package that we will use is called `os`

Run the following command in the main application directory
`> npm install os`

Your `package.json` file should have updated to look like this now:
```
  "dependencies": {
    "electron": "^5.0.5",
    "os": "^0.1.1",
    "path": "^0.12.7"
  }
```

in your main src > ipc > start.js file add the following lines:
```
const os = require('os')
process.env.USER_NAME = os.userInfo().username.toLowerCase()
```
This will set the process environment variable of USER_NAME to the current user that opened the application.

We can then use this value on the page for example, set it in the jquery object.
Open your `app_main.html` and change the value of the field to the process environment variable of USER_NAME like this:
```
$("#fld_name").val(process.env.USER_NAME)
```

your script should look like this now:
```
<script>
  require('../renderer/app_main_renderer.js')
  const { ipcRenderer } = require('electron')
  const _general = require('../js/document_models/_general')
  ipcRenderer.on('opened_main_page_reply', (event, arg) => {
    console.log(arg)
    _general.alerts.loaded()
    $("#fld_name").val(process.env.USER_NAME)
  })
</script>
```




Save all the files and open your command prompt in your application folder.
Run the following command :

`> npm start `



![Examples and lessons](https://github.com/Roche-Olivier/help.windows10.nodejs.electron.basics/blob/master/_content/_images/footer.png "Examples and lessons")



