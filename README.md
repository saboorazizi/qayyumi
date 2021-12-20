# qayyumi
## Create a repository (public) in GitHub
// private repository require us to authenticate
## Common Commands
> pwd (check current directory)
> ls (list directories)
> mkdir (make directory)
> cd DIRECTORY NAME (Navigate to a directory)
>>>> git config --global --unset credential.helper  (remove the cache incase if we need)
## Clone from GitHub
// download from GitHub and open it in commandline (easy way)
## To Clone and use Token Auth:
> git config --global credential.helper cache (set the cache to remember username and password)
> git clone https://github.com/saboorazizi/qayyumi.git
> Username for 'https://github.com': saboorazizi.82@gmail.com
> Password for 'saboorazizi.82@gmail.com': OUR Token Key



## Commit and Push
// repeate below commands to commit and push
> git init (xx Not Need it xx)
// Working Directory
> git status (modified files will be in red color)
// Local, Staging Area
> git add README.md   or > git add . (to add all files)
> git status (after "git add ." all modified files will be in green color)
// Commit
> git commit -m "first commit"
> git status (Nothing to commit, working directory clean)

> git remote add origin https://github.com/saboorazizi/qayyumi.git
> git push origin master

## Step 1. Install Mix
npm init -y
npm install -D laravel-mix

## Step 2. Create a Mix Configuration File
touch webpack.mix.js


## Step 3. Define Your Compilation
### // webpack.mix.js
// add below to webpack.mix.js
// Create folders also correct the app.js path


let mix = require('laravel-mix');
mix.js('src/js/app.js', 'dist').setPublicPath('dist');


### // Create a src/js/app.js and also src/scss/scss.scss and files
- wordpress-theme
    |--node_modules
    |--src
        ---js/app.js
        ---scss/app.scss
        ---css/optic-style.css 
        //costum css must not be here because we have tailwind.conf.js
    index.php
    style.css
    webpack.mix.js

## Step 4. Compile for test
// by running this code we create our dist folder 
npx mix

## Install Tailwindcss via npm

npm install -D tailwindcss@latest postcss@latest autoprefixer@latest

## Create our configuration file (tailwind.config.js)
npx tailwindcss init

## modify tailwind.config.js the purge part as below to recoganize our .php and .html files
  purge: {
    mode: 'layers',
    content: ['./*.php', './inc/**/*.php', './template-parts/**/*.php', './assets/**/*.js']
  },

## Creating our source css file
// add below lines to our src/scss/app.scss which is our source css

@import "tailwindcss/base";
@import "tailwindcss/components";
@import "tailwindcss/utilities";

## Compile JavaScript and Sass and Set the Output Base Directory
// Some modification to webpack.mix.js as below:
// laravel-mix.com

let mix = require('laravel-mix');
mix
    .js('src/js/app.js', 'js')
    .sass('src/scss/app.scss', 'css')
    .css('src/css/optic-style.css', 'css')
    .setPublicPath('dist')
    .options({
        postCss: [
            require('tailwindcss')
        ]
    })
    .browserSync({
        server: './public',
        files: ['./**/*.html', './dist'],
    });

// Install CROSS-ENV and set the host server from .env file so modify the browserSync as below:

    .browserSync({
        proxy: process.env.MIX_APP_HOST,
        host: process.env.MIX_APP_HOST,
        open: 'external',
        files: ['./**/*.html', './**/*.php', './dist'],
    });

## Install cross-env
npm install -D cross-env

## Create .env file
Create .env file in source directory and add below code

MIX_APP_HOST=localhost:3000/

## Compile Again
// by running this code we create our dist folder 
npx mix

## Watching for Changes
npx mix watch


## Create our own build/watch/prod Scripts
// In package.json we add the following scripts

  "scripts": {
    "build": "mix",
    "watch": "mix watch",
    "prod": "cross-env NODE_ENV=production npm run build"
  },

  // So now instead of running exteranl laravel-mix commands we run npm commands

  npx mix   === npm run build
  npx mix watch === npm run watch
  
  // Also by running "npm run prod" we can minimaiz our js and css files for production use


  ## Create


