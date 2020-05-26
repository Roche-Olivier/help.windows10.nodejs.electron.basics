### [![Index](https://github.com/Roche-Olivier/help.windows10.nodejs.electron.basics/blob/master/_content/_images/home.png "Index") Index](https://github.com/Roche-Olivier/help.windows10.nodejs.electron.basics)

## Adding jQuery

Open your `app_main.html` page , and add the following to the header section
```
  <!-- Insert this line above script imports  -->
  <script>
    if (typeof module === 'object') {
      window.module = module;
      module = undefined;
    }
  </script>
  <!-- JQuery -->
  <script src="https://code.jquery.com/jquery-3.4.1.min.js"
    integrity="sha256-CSXorXvZcTkaix6Yvo6HppcZGetbYMGWSFlBw8HfCJo=" crossorigin="anonymous"></script>
  <!-- Insert this line after script imports -->
  <script>
    if (window.module) module = window.module;
  </script>
```

You can then add all your other imports under that script.
You page header should look like this now:
```
<head>
  <meta charset="utf-8">
  <title>Hello World!</title>
  <!-- Insert this line above script imports  -->
  <script>
    if (typeof module === 'object') {
      window.module = module;
      module = undefined;
    }
  </script>
  <!-- JQuery -->
  <script src="https://code.jquery.com/jquery-3.4.1.min.js"
    integrity="sha256-CSXorXvZcTkaix6Yvo6HppcZGetbYMGWSFlBw8HfCJo=" crossorigin="anonymous"></script>
  <!-- Insert this line after script imports -->
  <script>
    if (window.module) module = window.module;
  </script>
</head>
```

Ok lets test this now, add an input field at the bottom of the body of the `app_main.html` page :
```
  <br>
  <input id="fld_name" type="text" value="First value">
```

Add the following script to the ipcRenderer.on process under your scripts section in the page
```
 $("#fld_name").val("Roche")
```
This will add the name 'roche' in the field that we added to the body.

Your `app_main.html` should look like this now:
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Hello World!</title>
  <!-- Insert this line above script imports  -->
  <script>
    if (typeof module === 'object') {
      window.module = module;
      module = undefined;
    }
  </script>
  <!-- JQuery -->
  <script src="https://code.jquery.com/jquery-3.4.1.min.js"
    integrity="sha256-CSXorXvZcTkaix6Yvo6HppcZGetbYMGWSFlBw8HfCJo=" crossorigin="anonymous"></script>
  <!-- Insert this line after script imports -->
  <script>
    if (window.module) module = window.module;
  </script>
</head>

<body>
  <h1>Hello World! This is example 5</h1>
  We are using node
  <script>document.write(process.versions.node)</script>,
  Chrome
  <script>document.write(process.versions.chrome)</script>,
  and Electron
  <script>document.write(process.versions.electron)</script>.
  <br>
  <input id="fld_name" type="text" value="First value">
</body>

<script>
  require('../renderer/app_main_renderer.js')
  const { ipcRenderer } = require('electron')
  const _general = require('../js/document_models/_general')
  ipcRenderer.on('opened_main_page_reply', (event, arg) => {
    console.log(arg)
    _general.alerts.loaded()
    $("#fld_name").val("Roche")
  })
</script>

</html>
```




Save all the files and open your command prompt in your application folder.
Run the following command :

`> npm start `

![Examples and lessons](https://github.com/Roche-Olivier/help.windows10.nodejs.electron.basics/blob/master/_content/_images/footer.png "Examples and lessons")



