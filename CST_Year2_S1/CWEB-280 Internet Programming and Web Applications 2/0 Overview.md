>Date: 2024 09 05
>Author: Denali

Projects (3) - 60%
Pair up
PHP 1990's style is first project, no JS on browser, only on the server side.
Database (SQLite) and JS frontend, react or u-JS.
Full stack 
Final Project - 40%
### Config
Apps anywhere
![](Pasted%20image%2020240901093607.png)
Install Node.Js
use nvm at home, use full at school.
We will not use the CMD, so you can close it.
Open normal CMD.
`node -v`
Should show a version, if not then it isn't install properly.
`npm -v`
Should do that same thing.

What is Node?
An application that runs JS on your server.
Express: Took the engine out of the chrome browser in 2009 to have it run JS files. This is the framework.

What is NPM?
Pull other peoples libraries from a repository.
Could use Barn, nmpn or something.
`npm i -g npm`
This will update NPM.

New project, express
![](Pasted%20image%2020240901093621.png)
Make sure it's named that, and uses that view engine.

Run from package.json.
Listening for us to make a request with out browser.
`localhost:3000`

Add to www to quickly go to website once you start application.
```JS
console.log("http://localhost:" + port);
```

DO NOT run JS on client side for the first LO / Assignment.

In the browser, you can look up:
`localhost:3000/something` to see the error.
`localhost:3000/users` does return something.

Paths are not linked to folder structure and based off your code.
In `app.js` you can see the paths and where they lead.
### More Tools
Linters, keep code sty;e normalized.
ESLint
```shell
npm init @eslint/config@1.0.0
```
Do this in the IntelliJ terminal.
Enter to proceed, space to change option.

3rd options
Common JS
None
No
Space both browser and node
Standard
Yes
Npm

![](Pasted%20image%2020240901094553.png)
Right click and at the bottom, or save on changes (ctrl + s).

Back to terminal
`npm i -D node-dev`

Change package.json line 6 to
```json
"start": "node-dev ./bin/www"
```
### Server side languages (not important)
1. PHP
2. Node.js
3. Python
4. Ruby
5. Java
### NPM
Look up NPM (something) to probably find it in a huge repository available online.
## Bootswatch theme
https://bootswatch.com/
https://cdnjs.com/libraries/bootswatch
https://cdnjs.cloudflare.com/ajax/libs/bootswatch/5.3.3/solar/bootstrap.rtl.min.css

`layout.hbs` to add solar style from bootswatch
```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/bootswatch/5.3.3/solar/bootstrap.rtl.min.css">
```
### Install locally
Terminal
`npm i bootstrap bootswatch`

Copy Path
![](Pasted%20image%2020240901094744.png)
`node_modules/bootswatch/dist`
```JS
app.use('/bw', express.static(path.join(__dirname, '/node_modules/bootswatch/dist')))
```

Can change the css link in the `layout.hbs` to run locally.
```
<link rel="stylesheet" href="/bw/quartz/bootstrap.css">
```