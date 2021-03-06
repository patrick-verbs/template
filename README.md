# Setting Up an Environment
##### _From lessons on [LearnHowToProgram.com](https://www.learnhowtoprogram.com/intermediate-javascript/test-driven-development-and-environments-with-javascript)_

---

## Overview

- __Node.js__ along with __Node Package Manager__ allows us to easily install and manage JavaScript packages in a project.

<details>
<summary><em>Install & update instructions</em></summary>

  - __Node.js__
    - Installing
      - __Mac install:__
        - If you followed the _Learn How to Program_ setup steps, you should have Homebrew installed (if not, check out [this guide](https://treehouse.github.io/installation-guides/mac/homebrew))
        - Open the Terminal and run `brew update` to have Homebrew find (but not yet install) the latest version of Node
        - After that, run `brew install node`
      - __Windows install:__
        - You can [download Node from the official website](https://nodejs.org/en/download/)
    - Updating
      - Check your version with: `node -v`
      - __Mac update (with Homebrew):__
        - If you used Homebrew to install it (see above), run:
          - `brew update`, then:
          - `brew upgrade node`
      - __Windows update & Mac update (without Homebrew):__
        -  
          
  - __Node Package Manager__ (npm)
    - Installing
      - Run: `npm install -g npm`
    - Updating
      - __Mac:__
        - Check your version with: `npm -v` (it might be good to make sure you & your pair are on the same version!)
        - Update with: `npm install -g npm` or `npm install -g npm@latest` (for the latest version)
      - __Windows:__
        - This can be tricky! Windows often installs npm in two different locations. [Check out this tool](https://github.com/felixrieseberg/npm-windows-upgrade#older-nodejs-versions) for how best to go about updating!
</details>
<br><br>

- __webpack__ is a _module bundler_ that will __concatenate__ and __minify__ our code. This is important because we can keep our code __readable__ (verbose syntax & separated logic/file structure) in our _development_ environment, then have __webpack__ condense everything into minimal (non-human-readable) file structure & code syntax for efficient loading/deployment in _production_ environments.
<details>
<summary><em>Install & update instructions</em></summary>

  - Installing
  - Updating
  - Plugins:
    - `html-webpack-plugin`: allows us to easily generate HTML templates.
    - `webpack-dev-server`: automatically reloads our code in the browser when we make changes to it!
  - Modules:
    - `eslint`: automatically notifies us when our code contains errors or is poorly-written. __It is crucial that this be loaded by webpack first, before our code is minified, so that it reads our human-readable code for errors.__ Counterintuitively, this means listing `eslint` __last__ in our "`rules:`" section of the webpack config file (as these rules are loaded in reverse order).
</details>
<br><br>

- __Jest__ allows us to run automated tests to ensure our code is working correctly.
<details>
<summary><em>Install & update instructions</em></summary>


</details>
<br><br>

---


## File Structure
##### _Based on information [detailed here](https://www.learnhowtoprogram.com/intermediate-javascript/test-driven-development-and-environments-with-javascript/future-project-structure)_
<details><summary><em>Example file layout with explanations</em></summary>

```
repository-name/
  |   (NOTE: the below folder/file structure is *non*-alphabetized to illustrate the workflow)
  |
  |
  ????????? src/  ???????????? *all* of our development (human-readable!) files live here: JS, HTML, CSS...
  |     |
  |     ????????? index.html
  |     ????????? main.js  ???????????? a common name for our "entry-point" JavaScript, which will import other JS files/functions as needed!
  |     ????????? circle.js   ????????????
  |     ????????? triangle.js  ???????????? example names for specific business-logic chunks of code, which main.js will call on.
  |     ????????? css/
  |           ????????? styles.css
  |
  |
  |
  ????????? __tests__/  ???????????? all of the tests we write go in this directory (note the four "_" used in the name)
  |     |
  |     ????????? circle.test.js  ???????????????
  |     ????????? triangle.test.js  ???????????? example tests (note both instances of the "." in each file name)
  |
  |
  |
  ????????? dist/  ???????????? our compiled *production* code (exclude this from GitHub repos, as the focus there should be on *development* code)
  |     |
  |     ????????? bundle.js  ???????????? webpack generates this file for us -- this should contain everything from the "src/" directory, all bundled up!
  |
  |
  |
  ????????? node_modules/  ???????????? this directory stores all of our project's dependencies -- it is auto-generated, downloading everything for us based on package.lock.json (see below)
  |
  |
  |
  ????????? package.json  ???????????? holds a list of all our project's *dependencies* (i.e., packages we need) so we can easily auto-install them
  ????????? package.lock.json  ???????????? auto-generated when we install our dependencies (see above) -- think of the "lock" as meaning "don't edit this!"
  |                             "package.lock.json" is basically just a *much* longer version of "package.json" (".lock" lists all the dependencies of our dependencies, and so on...)
  |
  |
  ????????? webpack.config.js  ???????????? this is where we tell webpack how to process & bundle our source code.
  |
  |
  |
  ????????? .gitignore  ???????????? you may already have a "global" .gitignore file, *but* every project should generally have its own here too!
  |                     Make sure to block "dist/" & "node_modules/" to prevent them from uploading to GitHub if you've compiled your code.
  |
  |
  ????????? .babelrc  ???????????? our Babel config file -- in general, it's used to make sure newer JS code works on old browsers. We use it to ensure Jest works properly.
  |
  |
  |
  ????????? .eslintrc  ???????????? and this is our ESLint config file -- ESLint takes the "pocket lint" out of our code, so to speak, and alerts us if we're writing code poorly.
  |
  |
  |
  ????????? README.md  ???????????? always :P
```

</details>


---
## Setup Steps

<details><summary><em><strong>Setup from scratch</em></strong></summary>

1. Name and create a new repository (`repository-name` will be the example in the code here)
2. Make your `src/`, `src/css/`, and `__test__` directories: <br>`$ mkdir src 'src/css' '__test__' `
3. Add your `README.md`, `index.html`, `main.js`, and `styles.css` files: <br>`$ touch README.md src/index.html src/main.js src/css/styles.css`
4. Add your <em>non-</em>auto-generated configuration files: <br>`$ touch package.json .gitignore webpack.config.js`
5. Fill in the starter code for `package.json`: <br>
```
{
  "name": "repository-name",
  "version": "1.0.0",
  "description": "",
  "main": "main.js",
  "scripts": {
    "build": "webpack"
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```
6. Install `webpack` using Node Package Manager (npm)
    - The "pinned" (recommended) version for Epicodus is v4.39.3:<br>`npm install webpack@4.39.3 --save-dev --save-exact`
    - This adds `webpack` to your `package.json` file, so you won't have to!
    - The `--save-dev` flag is important to ensure the __development__ version is installed
    - The `--save-exact` flag ensures that the __exact__ version we specified is installed to our dependencies (in the `node_modules/` folder)
7. Install `webpack-cli` (the __command line interface__ for webpack)<br>`$ npm install webpack-cli@3.3.8 --save-dev --save-exact`
8. Fill in some starter code for `.gitignore`, along with any other files you know you want to block!
```
node_modules/
dist/
.DS_Store
```

9. Fill in starter code for `webpack.config.js` as well:
    - The `entry: './src/main.js',` line means the `main.js` file is the "entry point" to all your other files -- in other words, the place where `webpack` will begin its recursive search for other files to add to `bundle.js`
    - You can change `bundle.js` will be placed in a `dist/` directory based on the `filename:` and `path:` lines
```
const path = require('path');

module.exports = {
  entry: './src/main.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  }
};
```


</details>

<br>

__To remove a dependency__:
  1. First try deleting its line from `packages.json`, then running `$ npm prune` to prune away modules that aren't listed there
  2. If that doesn't get the job done, trying deleting the line, then _deleting your `node_modules/` directory_, then rebuilding it with `$ npm install`



---
# _{A Template for Creating New Projects}_

#### _{Brief description of application}_

#### By _**{List of contributors}**_

## Technologies Used

* _List all_
* _the major technologies_
* _you used in your project_
* _here_

## Description

_{This is a detailed description of your application. Give as much detail as needed to explain what the application does as well as any other information you want users or other developers to have.}_

## Setup/Installation Requirements

* _This is a great place_
* _to list setup instructions_
* _in a simple_
* _easy-to-understand_
* _format_

_{Leave nothing to chance! You want it to be easy for potential users, employers and collaborators to run your app. Do I need to run a server? How should I set up my databases? Is there other code this application depends on? We recommend deleting the project from your desktop, re-cloning the project from GitHub, and writing down all the steps necessary to get the project working again.}_

## Known Bugs

* _Any known issues_
* _should go here_

## License

#### _{Chosen license}_

#### _Developer's Intent_

###### I am not an attorney and the following does not constitute legal advice. It is intended to convey my intent with the license by describing my understanding of it.

{"I chose this license because..."}

* _License does this_
* _License does that_

Please use this licensed software---or licensed non-software such as data, media, etc.---as follows:

* _Desired use-case_

Whether appropriately protected by the chosen license, please do not use this software or non-software work to:

* _Undesired use-case_

_{Let people know what to do if they run into any issues or have questions, ideas or concerns.  Encourage them to contact you or make a contribution to the code.}_

## Contact Information

_{Add your contact information here.}_