# Brunch + Bootstrap 4

This is a modern JS skeleton for [Brunch](http://brunch.io).

## Getting started

### Install (if you don't have them):
* [Node.js](http://nodejs.org): `brew install node` on OS X
    - For best compatibility install and use Node version 10.3.0 via Node Version Manager, NVM.
* [Brunch](http://brunch.io): `npm install -g brunch`
* Brunch plugins and app dependencies: `npm install`

### Run:
* `brunch watch --server` — watches the project with continuous rebuild. This will also launch HTTP server with [pushState](https://developer.mozilla.org/en-US/docs/Web/Guide/API/DOM/Manipulating_the_browser_history).
* `brunch build --production` — builds minified project for production

### Learn:
* `public/` dir is fully auto-generated and served by HTTP server.  Write your code in `app/` dir.
* Place static files you want to be copied from `app/assets/` to `public/`.
* [Brunch site](http://brunch.io), [Getting started guide](https://github.com/brunch/brunch-guide#readme)

---

## Node Version Manager

This section describes how to install and use Node Version Manager (NVM) on Windows and Apple
machines for managing and changing the version of Node being used on that machine.

Brunch recommends using Node version 10.3.0 and developers will need to be able to switch to 
this version to run and contribute to the kbhome-ui solution.

### Windows
* Install NVM for Windows:
    * Website: https://github.com/coreybutler/nvm-windows/releases
    * For new NVM installs, download the nvm-setup.zip file
    * Unzip this file and run nvm-setup.exe

* Use NVM for Windows:
    * In a Command Prompt, run the following commands:
        * List installed versions of Node:  `nvm ls`
        * Install a specific Node version:  `nvm install 10.3.0`
        * Use a specific Node version:  `nvm use 10.3.0`

### macOS
* Install NVM for macOS:
    * See https://tecadmin.net/install-nvm-macos-with-homebrew/ for instructions on installing NVM using Homebrew

* Use NVM for macOS:
    * In the terminal, run the following commands:
        * List all versions of Node available for installation: `nvm ls-remote`
        * List installed versions of Node: `nvm ls`
        * Install and use a specific version of Node: `nvm install v10.3.0`

---

## Adding a New Page

* Follow these basic steps for adding a new page to the site:
    1. Create a new .hbs file
    2. Create a new .scss file
    3. Add a new .scss file reference to index.scss
    4. Create a new .js file

* For example, to add a Search Results page:
    1. Add a new search-results.static.hbs file
    2. Add a new search-results.scss file
    3. Add a "@import './scss/search-results';" line item to index.scss
    4. Add a new search-results.js file

---

## Opening & Running the KB Home JSON Server project

* There is a standalone KB Home JSON Server application (Node.js) that can be found here: `https://kbhome.visualstudio.com/KBHomeCom2/_git/kbhome-json-server`
* Clone this repository into a new `kbhome-json-server` folder.
* Navigate to the /kbhome-json-server folder and type `npm install`.

* Note: JSON Server must run in a higher version of Node than the version 10.3.0 that Brunch and the kbhome-ui solution run on.
* In order to accomplish this, run the kbhome-json-server solution via one console window, and kbhome-ui solution in a second console window.
 
* To run both the JSON Server and kbhome-ui solutions:
    1. Open a console window (Run as Administrator on Windows) and navigate to your local /kbhome-json-server folder.
    2. Type `nvm ls` to see what versions of Node are installed on your machine.
    3. Type `nvm use 18.14.0` to change to a more recent version of Node (version 18.14.0 in this example).
    4. Start JSON Server (with custom routes) by entering: `npm start`
    5. Open a second console window (Run as Administrator on Windows) and navigate to the root kbhome-ui solution folder.
    6. Type `nvm ls` to see what versions of Node are installed on your machine, and which one is active.  It should say `14.16.0` in this example.
    7. Type `nvm use 10.3.0` to change to the version of Node required by Brunch (version 10.3.0).    
    8. Start the kbhome-ui solution per usual by entering: `brunch watch --server`

* Information about JSON Server can be found here : https://www.npmjs.com/package/json-server

---

## Troubleshooting
* After running `brunch watch --server` you may encounter the following error: "warn: Loading of sass-brunch failed due to Node Sass does not yet support your current environment: OS X 64-bit with Unsupported runtime (64)." To eliminate error you must update node-sass module. Use command `npm rebuild node-sass` (see https://stackoverflow.com/questions/37415134/error-node-sass-does-not-yet-support-your-current-environment-windows-64-bit-w for reference)

* Because we utilize `npm node-sass` in this project and that requires `node-gyp` / must be compiled locally, you may run into issues when running `npm install` for the first time - if that's the case make sure you have these tools, libraries for your platform:

    #### **Windows Specific**
    * Python - 2.x and your %PATH% variable set to the location of your python.exe (Python 3.x may also work, but this was tested with 2.x)
    * Visual Studio 2017 C++ Build Tools - even if you have VS 2019, 2022 or newer, you may still have to install the older 2017 C++ build tools for this project. That can be done by opening Visual Studio Installer, click `Modify` your installation, select `Individual Components` and search for `2017` - then choose the `build-tools` option for your architecture (eg: x64 or ARM)
    * With the above done if you still get errors during `npm install` run these two commands to set your npm config to look for the right versions of the C++ libraries. 
        * With Visual Studio: https://github.com/sass/node-sass/issues/2868#issuecomment-744338227
        * Without Visual Studio: https://github.com/nodejs/node-gyp - under the Windows section you can get the tools you need independently of Visual Studio

    ```
    npm config set msvs_version 2017
    npm config set msbuild_path "C:\Program Files (x86)\Microsoft Visual Studio\2019\Professional\MSBuild\Current\Bin\MSBuild.exe"
    ```

    NOTE: Be sure to change the build path according to your version of VS Studio (if you have VS)

    #### **Apple Specific**
    * You'll need to have Xcode command line tools installed on your machine - if you have Homebrew installed, you may not need this
        * Run `xcode-select --install` in Terminal
