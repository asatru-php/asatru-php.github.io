# npm/webpack

The framework supports npm and webpack to build your JavaScript and CSS files. Define
your JavaScript implementations in ‚dist/js/app.js‘ (you can also create other files which
can be imported into the app.js) and define your SASS rules in ‚dist/sass/app.scss‘ (you
can also create other files which can be imported into the file).

On a newly created project first run the command
```
npm install
```

This will install npm along with the required dependencies in the project.

Whenever you have finished something and want to build your work then run the
command
```
npm run build
```

You can also automatically check for changes and then let the system create an updated build:
```
npm run watch
```
 
This will bundle your SASS and JavaScript code into the app.js
in the ‚app/resources/js/app.js‘ file
