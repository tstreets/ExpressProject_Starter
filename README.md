# ExpressProject_Starter

## Table of Contents
- [Prereqs](#prereqs)
- [Setup](#setup)
  1. [Open Project](#open-project)
  2. [Initialize package.json](#initialize-package.json)
  3. [Create index.js](#create-index.js)
  4. [Install Dependencies](#install-dependencies)
- [Create Simple Server](#create-simple-server)
  1. [Require Modules Needed](#require-modules-needed)
  2. [Create the app](#create-the-app)
  2. [Create the server](#create-the-server)
  4. [View the server](#view-the-server)
  4. [Add content to the server](#add-content-to-the-server)
- [Setup Pug Engine](#setup-pug-engine)
  1. [Require new modules](#require-new-modules)
  2. [Configure app view engine](#configure-app-view-engine)
  3. [Create and run pug index](#create-and-run-pug-index)
  3. [Multiple pug pages](#multiple-pug-pages)
## Prereqs
- [Node js](https://nodejs.org/en/)
- [Heroku](https://devcenter.heroku.com/articles/heroku-cli)
- [Git](https://git-scm.com/downloads)
- Code Editor (eg: [Visual Studio Code](https://code.visualstudio.com/))

## Setup
### Open Project
Create a root folder for the project. Then open that folder in your code editor.\
*I'll be using Visual Studio Code and will refer to the editor as VScode in furture instances*

![Open Project](/Images/Open_Project.png)

### Initialize package.json
The package.json file is one of the most important files in any node js project. We'll create a simple one by typing this command into your terminal.\
*I'm using VScode's built-in terminal*

Terminal Command:\
`npm init -y`

### Create index.js
The index.js is going to be our main file for our app. Create this file it the root directory of the project.

![Root Directory](/Images/Index_JS.png)

### Install Dependencies
For all express projects you'll need to install express and a template view engine. I'll be using pug as my view engine and consolidate js to configure my view engine. I'll also use path js to join strings together as a path name. When we install these modules, we'll also save them as dependencies so that they can be used on an actual server.
1. Express
2. Pug
3. Consolidate
4. Path

Terminal Command:\
`npm i express pug consolidate path --save`

## Create Simple Server

### Require Modules Needed
In the index.js file, we're going to store the modules we want to use as variables. To get the server started in a simple way we'll just need the express moduel that we installed and the http module that is built-in the node modules folder that was created.

Code Snippet (index.js):
```javascript
const http = require('http');
const express = require('express');
```

### Create the app
Still in the index.js file, we're going to store the express app as a variable. This variable will handle interactions with the server.

Code Snippet (index.js):
```javascript
...

const app = express();
```

### Create the server
In the index.js file, we're going to create the server and tell it what port to listen to. This port is what will run our app.

Code Snippet (index.js):
```javascript
...

const port = 3000;

const server = http.createServer(app);
server.listen(port);
```

### View the server
To view the server, run this command into the terminal. Then open your browser to `localhost:3000`. To stop the server simply press `Ctrl+C` in the terminal. 

Terminal Command:\
`node index.js`

Right now we're not telling our app what content to load so any path will lead this this error.

![Simple Server](/Images/Simple_Server.png)

### Add content to the server

Let's fix this error by having it show a header tag, regardless of which page is accessed. We'll do this using the app's get listener. Listen for '\*\*', which is a wildcard used for any route, then send over our header tag. We'll add our code between our app variable and port variable.

Code Snippet (index.js):
```javascript
...

app.get('**', function(req,res,next) {
    res.send('<h1>Hi there!</h1>');
})

...
```

Now run your server again. You should see something like this.

![Simple Server With Content](/Images/Simple_Server_1.png)

## Setup Pug Engine

### Require new modules
We'll need to app variables for the consolidate module and path module. At the top of the index.js file, just below our express variable, we're going to require these two new modules.

Code Snippet (index.js):
```javascript
...

const engine = require('consolidate');
const path = require('path');
```

### Configure app view engine
Next we'll need to configure our app's view engine so that we can render pug files appropriately. In the index.js file, just below declaring our express app, we'll set our app's engine to pug using the engine variable we made. Then we tell our app where our pug files will be located and to use the pug engine that we set up.

Code Snippet (index.js):
```javascript
...

app.engine('pug', engine.pug);
app.set('views', path.join(__dirname, 'views'));
app.set('view engine', 'pug');

...
```

### Create and run pug index
First we'll create a 'views' folder in the main directory. Then in the 'views' folder, we'll create a pug file called 'index.pug'. So your directory should look like this.

![Pug Engine Directory](/Images/Pug_Engine_Directory.png)

We'll add just basic content to our page. In VScode, emmet can generate the base for our page by entering `!` then pressing `tab`. Add a header tag with content then your index.pug file should look like this.

Code Snippet (views/index.pug):
```pug
<!DOCTYPE html>
html(lang="en")
    head
        meta(charset="UTF-8")
        meta(name="viewport", content="width=device-width, initial-scale=1.0")
        title Document
    body
        h1 Hi there!
```

To run our new pug index page we'll change our app's get listener. It looked like this before.

Code Snippet (index.js):
```javascript
...

app.get('**', function(req,res,next) {
    res.send('<h1>Hi there!</h1>');
})

...
```

We need to change it to render our pug page instead. Instead of using `res.send`, we're going to use `res.render` so express knows to render from our pug 'views' folder.

Code Snippet (index.js):
```javascript
...

app.get('**', function(req,res,next) {
    res.render('index');
}

...
```

Now when you run your server, it should look like this again.

![Simple Server With Content](/Images/Simple_Server_1.png)

### Multiple pug pages
Cool so now we have an index page showing but lets make it more of a site. We'll add two more pages and navigate between them. In the `views` folder, create two pug files: `about.pug` and `contact.pug`. Put content in them like the `index.pug` file. Then add a nav tag to the body of each of the pug files. The nav should look like this.

Code Snippet (views/contact.pug):
```pug
<!DOCTYPE html>
html(lang="en")
    head
        meta(charset="UTF-8")
        meta(name="viewport", content="width=device-width, initial-scale=1.0")
        title Document
    body
        nav
            a(href="/") Home
            a(href="/about") About
            a(href="/contact") Contact
        h1 Contact
```

We need to setup new get listeners for our app. We'll add these before our current wildcard listener. We'll add one for contact then one for about. It will structured similarly. It should look like this.

Code Snippet (index.js):
```javascript
...

app.get('/contact', function(req,res,next) {
    res.render('contact');
})

app.get('/about', function(req,res,next) {
    res.render('about');
})

...
```

Now run your server and it should look like this. Try navigating between the pages.

![Multiple Pug Pages](/Images/Pug_Pages.png)
