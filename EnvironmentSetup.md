# Setting Up an Environment
##### _From lessons on [LearnHowToProgram.com](https://www.learnhowtoprogram.com/intermediate-javascript/test-driven-development-and-environments-with-javascript)_

---
## Overview
- __Node.js__ along with __Node Package Manager__ allows us to easily install and manage JavaScript packages in a project.
  - __Node.js__  ᐸ─── Node Package Manager needs this installed first
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

- __webpack__ is a _module bundler_ that will __concatenate__ and __minify__ our code. This is important because we can keep our code __readable__ (verbose syntax & separated logic/file structure) in our _development_ environment, then have __webpack__ condense everything into minimal (non-human-readable) file structure & code syntax for efficient loading/deployment in _production_ environments.
  - Installing
  - Updating
  - Plugins:
    - `html-webpack-plugin`: allows us to easily generate HTML templates.
    - `webpack-dev-server`: automatically reloads our code in the browser when we make changes to it!
  - Modules:
    - `eslint`: automatically notifies us when our code contains errors or is poorly-written. __It is crucial that this be loaded by webpack first, before our code is minified, so that it reads our human-readable code for errors.__ Counterintuitively, this means listing `eslint` __last__ in our "`rules:`" section of the webpack config file (as these rules are loaded in reverse order).

- __Jest__ allows us to run automated tests to ensure our code is working correctly.

---
## File Structure
##### _Based on information [detailed here](https://www.learnhowtoprogram.com/intermediate-javascript/test-driven-development-and-environments-with-javascript/future-project-structure)_
```
repository-name/
  |   (NOTE: the below folder/file structure is *non*-alphabetized to illustrate the workflow)
  |
  ├── src/  ᐸ─── *all* of our development (human-readable!) files live here: JS, HTML, CSS...
  |     |
  |     ├── index.html
  |     ├── main.js  ᐸ─── a common name for our "entry-point" JavaScript, which will import other JS files/functions as needed!
  |     ├── circle.js   ᐸ──┐
  |     ├── triangle.js  ᐸ─┴─ example names for specific business-logic chunks of code, which main.js will call on.
  |     └── css/
  |           └── styles.css
  |
  |
  ├── __tests__/  ᐸ─── all of the tests we write go in this directory (note the four "_" used in the name)
  |     |
  |     ├── circle.test.js  ᐸ───┐
  |     └── triangle.test.js  ᐸ─┴─ example tests (note both instances of the "." in each file name)
  |
  |
  ├── dist/  ᐸ─── our compiled *production* code (exclude this from GitHub repos, as the focus there should be on *development* code)
  |     |
  |     └── bundle.js  ᐸ─── webpack generates this file for us -- this should contain everything from the "src/" directory, all bundled up!
  |
  |
  ├── node_modules/  ᐸ─── this directory stores all of our project's dependencies -- it is auto-generated, downloading everything for us based on package.lock.json (see below)
  |
  |
  ├── package.json  ᐸ─── holds a list of all our project's *dependencies* (i.e., packages we need) so we can easily auto-install them
  ├── package.lock.json  ᐸ─── auto-generated when we install our dependencies (see above) -- think of the "lock" as meaning "don't edit this!"
  |                             "package.lock.json" file is basically just a *much* longer version of "package.json" (".lock" lists all the dependencies of our dependencies, and so on...)
  |
  ├── webpack.config.js  ᐸ─── this is where we tell webpack how to process & bundle our source code.
  |
  |
  ├── .gitignore  ᐸ─── you may already have a "global" .gitignore file, *but* every project should generally have its own here too!
  |                     Make sure to block "dist/" & "node_modules/" to prevent them from uploading to GitHub if you've compiled your code.
  |
  ├── .babelrc  ᐸ─── our Babel config file -- in general, it's used to make sure newer JS code works on old browsers. We use it to ensure Jest works properly.
  |
  |
  ├── .eslintrc  ᐸ─── and this is our ESLint config file -- ESLint takes the "pocket lint" out of our code, so to speak, and alerts us if we're writing code poorly.
  |
  |
  └── README.md  ᐸ─── always :P
```