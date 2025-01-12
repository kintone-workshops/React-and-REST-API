# ⚠️ THIS REPO IS ARCHIVED ⚠️
# ⚠️ DO NOT USE THIS WORKSHOP ANYMORE ⚠️
# UPDATED WORKSHOP: [kintone-workshops/React-x-REST-API-Workshop](https://github.com/kintone-workshops/React-x-REST-API-Workshop)
---

# React Workshop by [Kintone](https://kintone.dev/) - Version 3

## Overview of the Repo

| File                                                     | Path                                     | Purpose                                                                          | Need to Modify?    |
| -------------------------------------------------------- | ---------------------------------------- | -------------------------------------------------------------------------------- | ------------------ |
| 📗 [README.md]                                            | `README.md`                              | Notes on how to configure this Kintone x React App setup                         | _Nope_             |
| 📕 [Slides.pdf](Slides.pdf)                               | `Slides.pdf`                             | Slides for the workshop                                                          | _Nope_             |
| 📕 [Install_NodeJS.md](docs/Install_NodeJS.md)            | `docs/Install_NodeJS.md`                 | Step-by-step guide on how to install NodeJS & npm                                | _Nope_             |
| 📕 [Steps.md](docs/Steps.md)                              | `docs/Steps.md`                          | Step-by-step guide on how to setup the Kintone x React App                       | _Nope_             |
| 📕 [Debugging_Log.md](docs/Debugging_Log.md)              | `docs/Debugging_Log.md`                  | Common bugs & its solutions for this workshop                                    | _Nope_             |
| 📕 [Change_FieldCodes.md](docs/Change_FieldCodes.md)      | `docs/Change_FieldCodes.md`              | Guide on how to modify this codebase to use your own field codes.                | _Nope_             |
| [index.js](frontend/src/index.js)                        | `frontend/src/index.js`                  | Renders React code & passes it to index.html; `ReactDOM.render(...);`            | _Nope_             |
| [index.html](frontend/public/index.html)                 | `frontend/public/index.html`             | Homepage of the React App; `<div id="root"></div>`                               | _Nope_             |
| [App.js](frontend/src/App.js)                            | `frontend/src/App.js`                    | **Parent component** - Combines the list & form components                       | Yes! - Append POST |
| [getRecords.js](frontend/src/requests/getRecords.js)     | `frontend/src/requests/getRecords.js`    | Fetches Kintone records, transforms response, & returns array of list items      | _Nope_             |
| [ListRecords.js](frontend/src/components/ListRecords.js) | `frontend/src/components/ListRecords.js` | **List component** - Creates a list from the list items array                    | _Nope_             |
| [.env.example](backend/.env.example)                     | `backend/.env.example`                   | Template for `.env` file that holds your Kintone credentials                     | Yes! - Rename      |
| [server.js](backend/server.js)                           | `backend/server.js`                      | Sets up the Express server that routes API requests from the frontend to Kintone | Yes! - Append POST |
| [postRecord.js](frontend/src/requests/postRecord.js)     | `frontend/src/requests/postRecord.js`    | Passes the POST API request from React to Express server                         | Yes! - Code it     |
| [InputForm.js](frontend/src/components/InputForm.js)     | `frontend/src/components/InputForm.js`   | **Form component** - Create a form that submits a POST request                   | Yes! - Code it     |

## Let's POST Data to a Web Database From a React Component <!-- omit in toc -->

Thank you for attending our **Kintone x React** workshop!

## Outline <!-- omit in toc -->

* [Overview of the Repo](#overview-of-the-repo)
* [Get Started](#get-started)
* [Kintone Web Database & Credentials](#kintone-web-database--credentials)
  * [🚀 Getting your FREE Kintone Database](#-getting-your-free-kintone-database)
  * [Create a Kintone Web Database App](#create-a-kintone-web-database-app)
    * [Kintone API Token](#kintone-api-token)
    * [📺 How to Create a Kintone Database App | Video](#-how-to-create-a-kintone-database-app--video)
  * [🔐 Securely input your credentials in a `.env` file](#-securely-input-your-credentials-in-a-env-file)
* [Expected Results](#expected-results)
  * [Right After `npm install`](#right-after-npm-install)
  * [After Creating a `.env`](#after-creating-a-env)
  * [After Completing the POST Section](#after-completing-the-post-section)
* [Want the Slide Deck?](#want-the-slide-deck)
* [Guide on Installing Node.js & npm](#guide-on-installing-nodejs--npm)
  * [macOS with nodenv](#macos-with-nodenv)
  * [Windows with nvm-windows](#windows-with-nvm-windows)
  * [📺 Installing Node.js | Video](#-installing-nodejs--video)
* [Debugging - Let's Fix Those Problems 💪](#debugging---lets-fix-those-problems-)
  * [`npm install` command is not working](#npm-install-command-is-not-working)
  * [How do I get my Kintone Subdomain?](#how-do-i-get-my-kintone-subdomain)
  * [React not updating after updating `server.js`?](#react-not-updating-after-updating-serverjs)
  * [Error from `Terminal 2 - backend`?](#error-from-terminal-2---backend)
  * [No response when starting the Express server?](#no-response-when-starting-the-express-server)
  * [Got a `UnhandledPromiseRejectionWarning` error?](#got-a-unhandledpromiserejectionwarning-error)
  * [Got a `GAIA_IA02` error?](#got-a-gaia_ia02-error)

## Get Started

First, let's download the [ahandsel/React_Workshop_by_Kintone](https://github.com/ahandsel/React_Workshop_by_Kintone) Repo and go inside the folder.

```bash
cd Downloads

git clone https://github.com/ahandsel/React_Workshop_by_Kintone

cd React_Workshop_by_Kintone
```

```bash
ls

README.md   Slides.pdf   backend   frontend
```

Inside there should be two folders (`frontend` & `backend`) and a README file & Slides PDF.

Open the `React_Workshop_by_Kintone` folder in [VS Code](https://code.visualstudio.com/docs/getstarted/tips-and-tricks#_command-line)

```bash
code .
```

Let's open a terminal per folder.  
Then inside the folders, download the required packages with `npm install`.

|                      | Terminal 1 - Frontend                               | Terminal 2 - Backend                               |
| -------------------- | --------------------------------------------------- | -------------------------------------------------- |
| Go inside the folder | `cd ~/Downloads/React_Workshop_by_Kintone/frontend` | `cd ~/Downloads/React_Workshop_by_Kintone/backend` |
| What is inside?      | Code for the React App                              | Code for the Express server                        |
| Install packages     | `npm install`                                       | `npm install`                                      |
| Prep Tasks           |                                                     | Rename `.env.example` file to `.env` beforehand    |
| To run the scripts   | `npm start`                                         | `npm start`                                        |

### ⚡ Notes ⚡ <!-- omit in toc -->

⚡ React requires **Node ≥ 10.16** & **npm ≥ 5.6** ⚡
* Check the versions inside the `React_Workshop_by_Kintone` folder:
  * `node -v`
  * `npm -v`
* Not the correct versions or Confused? 🤔 → Check out the [Guide on Installing Node.js & npm](#guide-on-installing-nodejs--npm) Section

⚡ Note: Please ignore the package deprecation warnings ⚡

🔎 The `npm install` command installs the required dependencies defined in the package.json files (in both the [frontend](frontend/package.json) & [backend](backend/package.json) folders) and generates a node_modules folder with the installed modules.

## Kintone Web Database & Credentials

_Built for teamwork, designed by you_!

### 🚀 Getting your FREE Kintone Database

[bit.ly/KDP_NEW](http://bit.ly/KDP_NEW)
* ⚡ Only use lowercase, numbers, & hyphens in your subdomain
* ⚠ Do not use uppercase nor special characters

|                                          |                                          |
| ---------------------------------------- | ---------------------------------------- |
| ![SignUp-1.png](./docs/img/SignUp-1.png) | ![SignUp-2.png](./docs/img/SignUp-2.png) |

### Create a Kintone Web Database App

Let's create a Kintone App to list off your favorite [manga](https://en.wikipedia.org/wiki/Manga)s!

Here are the required fields & their configurations for our workshop:

| Field Type | Field Name | Field Code | Note               |
| ---------- | ---------- | ---------- | ------------------ |
| Text       | Title      | `title`    | The manga's title  |
| Text       | Author     | `author`   | The manga's author |

Confused? 🤔 → Check out the [How to Create a Kintone Database App](https://youtu.be/pRtfn-8cf_I) video 📺  

#### Kintone API Token

To generate an API Token for a Kintone App:

1. Go to the Kintone App
2. Go to the Gear icon ⚙️ (top right corner) > Open the App Settings page
3. Click on the **App Settings** Tab > Click on **API Token** settings
4. Click the `Generate` button to generate a token
5. Click the `Save` button (top left corner) to save the token setting
6. Finally, click the `Update App` button (top right corner) to implement the token setting change.

Confused? 🤔 → Check out the [Get the API Token](https://youtu.be/pRtfn-8cf_I?t=117) video clip 📺  

#### 📺 How to Create a Kintone Database App | Video

<p align="center">
  <a href="https://youtu.be/pRtfn-8cf_I">
    <img height="200" alt="How to Create a Kintone Database App YouTube Thumbnail"
      src="https://img.youtube.com/vi/pRtfn-8cf_I/hqdefault.jpg">
  </a>
</p>

### 🔐 Securely input your credentials in a `.env` file

In the `backend` folder, **rename** the `.env.example` to `.env`!

Then following the template, input your Kintone credentials.

`.env` template:

```.env
SUBDOMAIN = ""
APPID = ""
APITOKEN = ""
```

Here is an example `.env` file.

```.env
SUBDOMAIN = "example"
APPID = "1"
APITOKEN = "dXNlckBleGFLtcGxlmNvbTpzZWNyZXQe9q3IhtcG"
```

---

## Expected Results

Here are the expected results after running the `npm start` in both the terminals.

### Right After `npm install`

|                  | Terminal 1 - Frontend                                                                                                | Terminal 2 - Backend                                                                                                 |
| ---------------- | -------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| View Results     | [localhost:3000](http://localhost:3000/)                                                                             | On the Terminal                                                                                                      |
| Expected Results | ![React_v3_img/Terminal_1_A.png](https://github.com/ahandsel/img/blob/master/React_v3_img/Terminal_1_A.png?raw=true) | ![React_v3_img/Terminal_2_A.png](https://github.com/ahandsel/img/blob/master/React_v3_img/Terminal_2_A.png?raw=true) |

### After Creating a `.env`

|                  | Terminal 1 - Frontend                                                                                                | Terminal 2 - Backend                                                                                                 |
| ---------------- | -------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| View Results     | [localhost:3000](http://localhost:3000/)                                                                             | [localhost:5000/getData](http://localhost:5000/getData)                                                              |
| Expected Results | ![React_v3_img/Terminal_1_B.png](https://github.com/ahandsel/img/blob/master/React_v3_img/Terminal_1_B.png?raw=true) | ![React_v3_img/Terminal_2_B.png](https://github.com/ahandsel/img/blob/master/React_v3_img/Terminal_2_B.png?raw=true) |

### After Completing the POST Section

|                  | Terminal 1 - Frontend                                                                                                | Terminal 2 - Backend |
| ---------------- | -------------------------------------------------------------------------------------------------------------------- | -------------------- |
| View Results     | [localhost:3000](http://localhost:3000/)                                                                             | n/a                  |
| Expected Results | ![React_v3_img/Terminal_1_C.png](https://github.com/ahandsel/img/blob/master/React_v3_img/Terminal_1_C.png?raw=true) | n/a                  |

---

## Want the Slide Deck?

Check it out at [Slides.pdf](Slides.pdf)

---

## Guide on Installing Node.js & npm

* [macOS with nodenv](#macos-with-nodenv)
* [Windows with nvm-windows](#windows-with-nvm-windows)
* [📺 Installing Node.js Video](#-installing-nodejs--video)

### Check if you already have Node.js or npm <!-- omit in toc -->

React requires **Node ≥ 10.16** & **npm ≥ 5.6**  
Go **inside** the `React_Workshop_by_Kintone` folder.

```shell
$ node -v
$ npm -v
```

If Node & npm are missing, let's install them!

**Options**:

* [macOS with nodenv](#macos-with-nodenv)
* [Windows with nvm-windows](#windows-with-nvm-windows)

### macOS with [nodenv](https://github.com/nodenv/nodenv)

We recommend installing Node.js using [nodenv](https://github.com/nodenv/nodenv) to manage node versions. This allows your computer to have a specific Node.js version per project.

⚠️ Remove any existing installations of Node.js before installing nodenv! ⚠️  
Having different Node.js installations can lead to conflict issues.

**Step 1**: Install nodenv with [Homebrew](https://brew.sh/)

|                 |                               |
| --------------- | ----------------------------- |
| Update Homebrew | `brew update && brew upgrade` |
| Install nodenv  | `brew install nodenv`         |

**Step 2**: Set up nodenv shell integration

|                                                       |                           |
| ----------------------------------------------------- | ------------------------- |
| Run the initialization command                        | `nodenv init`             |
| Append the following line into the shell's rc/profile | `eval "$(nodenv init -)"` |

| For Zsh users                                | For Bash users                                      |
| -------------------------------------------- | --------------------------------------------------- |
| `echo 'eval "$(nodenv init -)"' >> ~/.zshrc` | `echo 'eval "$(nodenv init -)"' >> ~/.bash_profile` |
| `cat < ~/.zshrc`                             | `cat < ~/.bash_profile`                             |

**Step 3**: Implement the changes

Close & open a new Terminal window for the changes to take place.

Optional: Verify that nodenv is properly set up using [nodenv-doctor](https://github.com/nodenv/nodenv-installer/blob/master/bin/nodenv-doctor) script.

* For those using Z shell (Zsh) shell:

    ```shell
    curl -fsSL https://github.com/nodenv/nodenv-installer/raw/master/bin/nodenv-doctor | bash
    ```

* Expected result:

    ```shell
    Checking for `nodenv' in PATH: /usr/local/bin/nodenv
    Checking for nodenv shims in PATH: OK
    Checking `nodenv install' support: /usr/local/bin/nodenv-install (node-build 3.0.22-4-g49c4cb9)
    Counting installed Node versions: none
      There aren't any Node versions installed under `~/.nodenv/versions'.
      You can install Node versions like so: nodenv install 2.2.4
    Auditing installed plugins: OK
    ```

**Step 4**: Install Node.js inside the React Workshop folder (`React_Workshop_by_Kintone`)

* Now you're ready to install specific Node.js versions!
* **Inside** `React_Workshop_by_Kintone` folder, install Node.js version `14.5.0`:

  ```shell
  cd React_Workshop_by_Kintone/

  nodenv install 14.5.0

  nodenv local 14.5.0
  ```

Alright! Your Mac is now armed with Node.js!

Download the required packages by going opening a terminal inside the `frontend` folder & `backend` folder & running the `npm install` command!

---

### Windows with [nvm-windows](https://github.com/coreybutler/nvm-windows#node-version-manager-nvm-for-windows)

The following steps are straight from the Microsoft Docs on [Set up NodeJS on native Windows](https://docs.microsoft.com/en-us/windows/dev-environment/javascript/nodejs-on-windows). We recommend installing and managing Node.js with [nvm-windows](https://github.com/coreybutler/nvm-windows#node-version-manager-nvm-for-windows)

⚠️ Remove any existing installations of Node.js before installing nvm-windows! ⚠️  
Having different Node.js installations can lead to conflict issues.

**Step 1**: Go to the [windows-nvm's latest release](https://github.com/coreybutler/nvm-windows/releases).

**Step 2**: Download the **nvm-setup.zip** file for the most recent release.

**Step 3**: Once downloaded, open the zip file, then open the **nvm-setup.exe** file.

**Step 4**: The Setup-NVM-for-Windows installation wizard will walk you through the setup steps, including choosing the directory where both nvm-windows and Node.js will be installed.

* ![install-nvm-for-windows-wizard.png](https://github.com/ahandsel/img/blob/master/Node_Install/install-nvm-for-windows-wizard.png?raw=true)

**Step 5**: After the installation is complete, open PowerShell & enter `nvm ls`

* `nvm ls` lists out installed Node versions (should be none at this point)
* ![windows-nvm-powershell-no-node.png](https://github.com/ahandsel/img/blob/master/Node_Install/windows-nvm-powershell-no-node.png?raw=true)

**Step 6**: Install Node.js inside the React Workshop folder (`React_Workshop_by_Kintone`)

* Now you're ready to install specific Node.js versions!
* Inside `React_Workshop_by_Kintone` folder, install Node.js version `14.5.0`:

  ```powershell
  cd .\Documents\React_Workshop_by_Kintone

  nvm install 14.5.0

  nvm use 14.5.0
  ```

Alright! Your Windows is now armed with Node.js!

Download the required packages by going opening a terminal inside the `frontend` folder & `backend` folder & running the `npm install` command!

### 📺 Installing Node.js | Video

<p align="center">
  <a href="https://youtu.be/4Kw-i_rX3tY">
    <img height="200" alt="Installing Node.js & Create a New React App YouTube Thumbnail"
      src="https://img.youtube.com/vi/4Kw-i_rX3tY/hqdefault.jpg">
  </a>
</p>

---

## Debugging - Let's Fix Those Problems 💪

Here is a rundown of common problems that may occur & its solutions!  

### `npm install` command is not working

1. Verify the Node.js & npm versions **inside** the `React_Workshop_by_Kintone` folder
2. Just installed Node.js? Verify you configured Node.js versions **inside** the `React_Workshop_by_Kintone` folder

* Mac: `nodenv local 14.5.0`
* Windows: `nvm use 14.5.0`

### How do I get my Kintone Subdomain?

It might be a bit confusing since you need to sign-up for [Developer Program Account (Website) 🌐](https://bit.ly/KDP_signup) BEFORE creating your [Kintone Subdomain (Database) 📂](http://bit.ly/K_DevLic).

Check out our [Sign up for Kintone Developer Program & Developer License](https://youtu.be/Gzz8SbTuoFg) YouTube video:

* [![https://youtu.be/Gzz8SbTuoFg](https://img.youtube.com/vi/Gzz8SbTuoFg/mq1.jpg)](https://youtu.be/Gzz8SbTuoFg)

### React not updating after updating `server.js`?

After making changes to `server.js`, be sure to restart the Express server On the `Terminal 2 - backend`!

* Stop the server: `ctrl + c`
* Start the server: `npm start`

Then reload the browser showing the React App: [localhost:3000](http://localhost:3000/)

### Error from `Terminal 2 - backend`?

Do you see an error on `.../React_Workshop_by_Kintone/backend/node_modules/node-fetch/lib/index.js:272` like the following?

```text
return Body.Promise.reject(new FetchError(`invalid json response body at ${_this2.url} reason: ${err.message}`, 'invalid-json'));
                           ^
FetchError: invalid json response body at https://r.kintone.com/notfound/subdomain.html reason: Unexpected token < in JSON at position 0
    at /Users/g001494/Downloads/React_Workshop_by_Kintone/backend/node_modules/node-fetch/lib/index.js:272:32
    at processTicksAndRejections (node:internal/process/task_queues:96:5)
    at async /Users/g001494/Downloads/React_Workshop_by_Kintone/backend/server.js:43:24 {
  type: 'invalid-json'
}
```

This error is related to your Kintone credentials.

1. Verify that you have created a `.env` file with your Kintone credentials inside the `backend` folder
2. Verify the Kintone credentials are correct: Subdomain, App ID, and API Token
3. Verify that the Kintone App is configured as done in the [Create a Kintone Web Database App](#create-a-kintone-web-database-app) section
4. Verify that the Kintone Web Database App is updated after generating the [Kintone API Token](#kintone-api-token)

### No response when starting the Express server?

1. Make sure you are inside the `backend` folder when starting the Express server.
   * `cd ~/Downloads/React_Workshop_by_Kintone/backend`
   * `npm start`
2. Verify that you have renamed `.env.example` to `.env`
   * Be sure to enter your Subdomain, App ID, and API Token in the `.env` file

### Got a `UnhandledPromiseRejectionWarning` error?

```text
(node:5379) UnhandledPromiseRejectionWarning: FetchError: request to https://.kintone.com/k/v1/records.json?app= failed, reason: getaddrinfo ENOTFOUND .kintone.com
```

* It looks like Kintone API credentials are missing
* Be sure to enter your Subdomain, App ID, and API Token in the `.env` file
* Confused? 🤔 → Check out the [🔐 Securely input your credentials in a `.env` file](#-securely-input-your-credentials-in-a-env-file) section

### Got a `GAIA_IA02` error?

* Enter the App's API Token in `.env` file as `APITOKEN = ""`
* Be sure to hit the `save` button & the `Update App` button to implement the API Token change.
