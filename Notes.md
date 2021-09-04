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
  
Basic TypeScript types:
- `string`: string types, textual data.
- `number`: number types incl. integers and decimals.
- `boolean`: `true`/`false`.
- Union types: more than one type can be used.
    ```ts
    let studentPhone: (number | string);
    ```
- `null` and `undefined`.
- `void`: used as a return type when the function returns nothing.
- `never`: used as a return type when the function will never return anything.
- `any`: should be avoided. Used when the type of the item being typed can be anything.
- `unknown`: used when the type of the thing being typed is unknowned. Used heavily for type assertion.
- `Array`: to type as an array, use the type, followed by square brackets.
    ```ts
    let arr: string[]; // only accepts strings
    let arr2: (string | number)[]; // accepts strings and numbers
    ```
- `Tuple`: tuples are not native to JavaScript. When you know exactly what data will be in the array, and you will not be adding to the array or modifying the type of any value, you can use a tuple.
    ```ts
    let arr: [string, number, string]; // ['cat', 7, 'dog']
    ```
- `enum`: enums are not native to JavaScript but are similar to enumerations used in other languages like C++ and Java. You use an enum when you have a constant set of values that will not be changed. By default, the values in an enum are also given a numeric value starting at 0. However, the numeric value can manually be set to any number explicitly or by calculation. Uses PascalCase to name the type.
    ```ts
    enum Weekend = { Saturday, Sunday};
    ```

**Interface**: With TypeScript, interfaces are simply used as the blueprint for the shape of something. Interfaces can be used to create functions but are most commonly seen to create objects. Use PascalCase for naming interfaces.

**Optional** and `readonly` properties:
- Optional: use when an object may or may not have a specific property by adding a `?` at the end of the property name.
    ```ts
    interface Student {
        name: string,
        age: number, 
        enrolled: boolean,
        phone?: number // phone is optional
    }
    ```
- `readonly`: use when a property mustn't be modified after the object has been created. Keep in mind that this will only produce TypeScript errors and that the actual properties can still technically be changed as read-only does not exist in JavaScript.
    ```ts
    interface Student { 
        name: string, 
        age: number, 
        enrolled: boolean,
        readonly id: number // id is readonly
    }
    ```

**Type aliases** do not create a new type; they rename a type. Therefore, you can use it to type an object and give it a descriptive name. But like the object type, once a type alias is created, it can not be added to; it can only be extended. Meaning, if you wanted to create an object from a type alias and then a second with additional properties, you would need to extend the type alias and make your second object with the extended alias. This makes interfaces the preferred method for creating objects.
```ts
type Student = {
    name: string,
    age: number,
    enrolled: boolean;
}

let newStudent: Student = {
    name: 'Maria',
    age: 10,
    enrolled: true
}
```

**Factory functions**: To create a factory function with explicit typing, create an interface with the object's properties and methods and use the interface as the return type for the function.
```ts
interface Student {
    name: string,
    age: number,
    greet(): void
}

const studentFactory = (name: string, age: number): Student => {
    const greet = ():void => console.log('hello');
    return { name, age, greet };
}

const myStudent = studentFactory('Hana', 16);
```

**Generics**:
- Reusable components that can be used with different types.
- *types* as *parameters*. Use angle bracket syntax `<T>` where `T` is the type parameter.
```ts
// Generic function
const getItem = <T>(arr: T[]): T => { return arr[0]; }

// Typed function
const getItem = (arr: number[]): number => { return arr[0]; }
```

**Asynchronous TypeScript**:
- `async / await` always return a `Promise`. `Promise`s are built-in objects that have their own properties and methods. 
- Use `Promise<type>` to set the type returned. 
```ts
const myFunc = async (): Promise<void> => { // do stuff };
```

To create Type definitions when one is missing while using third-party modules
- Create a `types` folder in your root directory with a subfolder specifically for `thirdParty` types.
- Create a file in the `thirdParty` folder called `index.d.ts`.
- Within your definition file, import the node module with the missing definition.
- Use the `declare` keyword.
- Write the definition which will likely be a class or an interface for a function.
- Open `tsconfig.json` and find `"typeRoots"` to include the new types directory.
```ts
// example
import _ from 'lodash';

declare module 'lodash' {
    interface LoDashStatic {
        multiply(multiplier: number, multiplicand: number): number;
    }
}
```

TypeScript best practices:
- Use `noImplicitAny` in `tsconfig.json` to prevent errors created by Typescript assuming `any` type.
- Turn on all `strict` checking by setting `strict` to `true` in your `tsconfiig.json` settings.
- Pay attention to when to use Implicit or Explicit typing.
    - `const`: **Implicit** typing. Value is immutable so type can't be changed.
    - `let`: **Explicit** typing. Value and type can be changed.
    - Function with controlled inputs: **Implicit** typing. Output is controlled and code is simpler.
    - Single-line arrow function: **Implicit** typing. Simplier code.
    - Longer function: **Explicit** typing. Easier to read.
- Use the latest EcmaScript features.

**Behavior-Driven Development** is a development style built on Test Driven Development where the focus is user interaction and stakeholders.

**Test-Driven Development** is a development style well suited for backend development. It focuses on writing unit and integration tests that produce expected results. Test-driven development follows a development cycle. This cycle continues until the feature is complete. The tests remain in the codebase and as the feature is built upon or other features are added, the tests will ensure the feature continues to work as expected and will quickly alert the development team to any potential conflicts or bugs.
- A feature request comes in.
- Tests are written for the most simple functionality of the feature that includes edge cases and failure expectations.
- Tests fail due to lack of code.
- Code is written to make tests pass.
- Code is refactored to be most concise and easy to read.

![test_driven_development_cycle](https://github.com/leovantoji/fullstack_js_dev_nanodegree/blob/main/images/fsjs-c1-l3-tdd-cycle.jpg)

**Expert Approach to Testing**:
- Start with the simplest tests to identify any major failures early on.
- Add tests for more complex situation and edge cases.
- Test for graceful error handling.
- Add more tests as needed.

**Test Design Best Practices**
- Test file structure and file names should match the app.
- Describe and name the tests to be easy to read and maintain.
- Design app features with pseudo code to inform tests.
    - Pseudo code provides an overview of the application complexity and finds the easiest pieces of the test to write, build, refactor, and reiterate.
- DRY (Don't Repeat Yourself)
    - Write short tests that allow you to pinpoint why the test is failing.
    - Try writing short, uncomplicated tests by first starting with an object with data that should pass and test each value in the object.
    - Try this again with an object with data that should fail unless the appropriate error is passed to ensure error handling is a standard, not an afterthought.
- Tests should be reliable.
    - Tests should only fail when there are bugs in the tested code.
    - Avoid conflicts with other tests.
    - Call the correct objects for each test. The wrong objects may have the wrong input and create an error.
    - Import the correct file for the test to avoid errors.

Running Jasmine after code has compiled to JavaScript:
![jasmine](https://github.com/leovantoji/fullstack_js_dev_nanodegree/blob/main/images/fsjs-c1-l3-jasmine.jpg)

Installing Jasmine and setting up the testing file structure for testing.
- Configuring Jasmine:
    - Install Jasmine: `npm i jasmine`.
    - Add a reporter for outputting Jasmine results to the terminal: `npm i jasmine-spec-reporter`.
    - Add type definitions for Jasmine with: `npm i --save-dev @types/jasmine`.
- Add testing scripts in `scripts` objects in the `package.json` file: `"jasmine": "jasmine"`.
- Set up the file structure:
```
├── node_modules
├── spec
│      ├──  support
│      └── jasmine.json
├── src
│     ├──  tests
│     │     ├── helpers
│     │     │      └── reporter.ts
│     │     └── indexSpec.ts
│     └── index.ts
├── package-lock.json
├── package.json
└── tsconfig.json
```

Best practices for file naming: When creating files for tests, a best practice is to name the `.ts` file the same as the `.js` file to be tested with `Spec` appended to the end. The more tests needed to be run, the more test files will need to be created. Be sure to follow this best practice to keep track of the test file that contains the tests for each `.js` file.











