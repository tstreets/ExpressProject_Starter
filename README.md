# ExpressProject_Starter

## Table of Contents
- [Prereqs](#)
- [Setup](#)
  1. [Open Project](#)
  2. [Initialize package.json](#)
  3. [Create index.js](#)
  4. [Install Dependencies](#)

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

`npm i express pug consolidate path --save`

## Create Simple Server

### Require Modules Needed

```javascript
const http = require('http');
const express = require('express');
```

