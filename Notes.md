# Udacity Full Stack Javascript Developer Nanodegree

## Prerequisite courses:
- [x] [Linux Command Line Basics](https://www.udacity.com/course/linux-command-line-basics--ud595)
- [x] [Intro to Java Script](https://www.udacity.com/course/intro-to-javascript--ud803)
- [ ] [JavaScript and the DOM](https://classroom.udacity.com/courses/ud117)
- [x] [Object-Oriented JavaScript](https://classroom.udacity.com/courses/ud711)
- [x] [Intro to HTML and CSS](https://classroom.udacity.com/courses/ud001)

## Backend Development with Node.js
Objectives:
- [ ] Setup and install a NodeJS environment to run server-side javascript and setup NPM to create project dependencies. 
- [ ] Write valid, clear TypeScript.
- [ ] Deploy unit tests with Jasmine.
- [ ] Build a server with Express.

The backend is responsible for processing the requests that come into the app and managing its data. A backend consists of three parts:
- **The server**: the computing resource that listens to requests from the frontend.
- **The application**: code that runs on the server to process requests and return responses.
- **The database**: the part of the backend that is responsible for storing and organizing data.

Stakeholders for backend development:
![stakeholders_backend](https://github.com/leovantoji/fullstack_js_dev_nanodegree/blob/main/images/fsjs-c1-l0-stakeholders.jpg)

Good use cases for Node.js include: eCommerce, blogging, chat apps, social networking, simple games, and content management systems. Node.js is **NOT** well-suited for applications that require heavy processing and computation, like video processing, 3D games, and traffic mapping.

Node.js uses Google's V8 engine as a runtime to process JavaScript.
![v8_stack](https://github.com/leovantoji/fullstack_js_dev_nanodegree/blob/main/images/fsjs-c1-l1-v8-stack.jpg)

Export JavaScript from file(s). It's common to see shorthand property in use.
```js
// working file = util/logger.js

// exports as objects
module.exports = {
    myFirstFunction: myFirstFunction,
    mySecondFunction: mySecondFunction
}

// using ES6 shorthand property names
module.exports = {
    myFirstFunction,
    mySecondFunction
}
```

**Path module** allows us to normalize paths to work across platform.
```js
const path = require('path');
```
- `path.resolve` gets the absolute path from a relative path.
- `path.normalize` normalizes any path by removing instances of `.`, turning double slashes into single slashes and removing a directory when `..` is found.
- `path.join` concatenates strings to create a path that works across operating systems. It joins the strings then normalizes the result.

**File system module** enables reading and writing to files with many options.
```js
const fs = require('fs');
```

**HTTP/HTTPS** module is used to transfer data.

**URL** module is used for parsing and resolving URLs.

**TLS/SSL** implements security protocols on top of OpenSSL.

Six phases of the **Event Loop**:
- Timers - executes callbacks using timers. If there are timers set to `0 ms` or `setImmediate()`, they will run here. Incomplete timers will run in later iterations of the loop.
- Pending - *internal phase*
- Idle/Prepare - *internal phase*
- Poll - process I/O callbacks.
- Check - execute any `setImmediate()` timers added in the Poll phase.
- Close - loop continues if there are more timers or I/O calls. If all timers and I/O calls are done, the loop closes and the process ends.

![event_loop](https://github.com/leovantoji/fullstack_js_dev_nanodegree/blob/main/images/fsjs-c1-l1-event-loop.jpg)

**Node Package Manager (NPM)** is both a **tool for managing project dependencies** via command line and a **website hosting more than 1 million third-party packages**.
- Modules are shared as packages.
- Packages extend the functionality of your app.
- Modules are stored in the app's `node_modules` folder.
- Core modules include `path`, `Filesystem`, and more.

General steps to work on NPM project:
- Initialize NPM: `npm init` (normal) and `npm init -y` (default settings)
- Adding dependencies (e.g. `prettier`):
  ```
  npm i prettier // install prettier
  npm i --save-dev prettier // install to dev dependencies
  npm i --save-dev prettier@2.2.1 // install a specific version of prettier
  ```
- Using dependencies (e.g. `prettier`): 
  - Add a `prettier` script to `package.json` file.
  - Create a `.prettierrc` file for any custom configurations.
  - Run `npm run prettier` to run `prettier`.
  
