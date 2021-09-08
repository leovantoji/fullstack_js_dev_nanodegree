# Udacity Full Stack Javascript Developer Nanodegree

## Prerequisite courses:
- [x] [Linux Command Line Basics](https://www.udacity.com/course/linux-command-line-basics--ud595)
- [x] [Intro to Java Script](https://www.udacity.com/course/intro-to-javascript--ud803)
- [ ] [JavaScript and the DOM](https://classroom.udacity.com/courses/ud117)
- [x] [Object-Oriented JavaScript](https://classroom.udacity.com/courses/ud711)
- [x] [Intro to HTML and CSS](https://classroom.udacity.com/courses/ud001)

## Backend Development with Node.js
Objectives:
- [x] Setup and install a NodeJS environment to run server-side javascript and setup NPM to create project dependencies.
- [x] Write valid, clear TypeScript.
- [x] Deploy unit tests with Jasmine.
- [x] Build a server with Express.

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

Suites and Specs:
- **Spec**: an individual test.
- **Suite**: a collection of similar tests related to one function.
- Tests should cover all intended behaviors.
- Error handling should also be tested.
![suites_specs](https://github.com/leovantoji/fullstack_js_dev_nanodegree/blob/main/images/fsjs-c1-l3-suites-and-specs.jpg)

Jasmine Syntax:
- Use the `describe` keyword followed by a short description of what the suite is testing and one or more specs.
- A best practice is to start a sentence with *it* and then complete the sentence with the description of what the suite is testing.
```jasmine
describe("suite description", () => {
    it("describes the spec", () => {
        const myVar = true;
        expect(myVar).toBe(true);
    });
});
```

Test types:
- Truthiness:    
    - `.toBeTruthy()` passes when:
        - The expectation has any non-zero value.
        - The expectation evaluates to `true`.
    - `.toBeFalsy()` passes when the value is:
        - `0`
        - `''` (an empty string)
        - `undefined`
        - `null`
        - `NaN`
    - If you just need the Boolean value of `false`, use `.toEqual()`
- Numerical Matchers:
    - `.toBeCloseTo(expected value, precision)
        - passes if a value is within a specified precision of the expected value.
        - precision is optional and represents the number of decimal points to check (default to 2).
    - `toBeGreaterThan(expected value)`
    - `toBeLessThan(expected value)`
    - `toBeGreaterThanOrEqual(expected value)`
    - `toBeLessThanOrEqual(expected value)`
- Negating Other Matchers: `!` in JavaScript, `not` in TypeScript, and `.not` in Jasmine.
- Exceptions:
    - `.toThrow(expected value)`
    - `.toThrowError(expected value, expected message)` (expected value and expected message are optional)
- Other Matchers:
    - `.toContain(expected value)`
    - `.toMatch(expected value)`
    - `.toBeDefined()`
    - `.toBeUndefined()`
    - `.toBeNull()`
    - `.toBeNan()`

An **endpoint** is the **URL** of the **REST API** with the method that *gets*, *adds to*, or *modifies* the data of an API in some way.
![endpoint](https://github.com/leovantoji/fullstack_js_dev_nanodegree/blob/main/images/fsjs-c1-l3-endpoint.jpg)

Benefits of endpoint testing:
- Confirms that the server is working.
- Confirms that endpoints are configured properly.
- More efficient than manual testing.

Endpoint testing is not native to Jasmine and requires a 3rd party framework, like `supertest` to test the status of responses from server.
- Install `supertest` as a dependency: `npm i supertest`
- Add type definition to allow the code to compile without TypeScript errors: `npm i --save-dev @types/supertest`
- Import `supertest` in the `spec` file.
```ts
import supertest from 'supertest';
import app from '../index';

const request = supertest(app);
describe('Test endpoint responses', () => {
    it('gets the api endpoint', async (done) => {
        const response = await request.get('/api');
        expect(response.status).toBe(200);
        done();
    }
)});
```

Setup and Teardown of Suites are Jasmine features that allow you to:
- Connect to a database before a test.
- Connect to a different database for specific tests.
- Run only a specific test.
- Skip one or more tests.
- `beforeEach` takes a callback function where we can tell the test to perform a task **before each test is run**.
- `afterEach` is used if there is a task to be run **after each test is run**.
- `beforeAll` is used if there is an operation to be run **once before** running all the specs in a suite.
- `afterAll` is used if there is an operation to be run **once after** running all the specs in a suite.

![beforeEach_afterEach](https://github.com/leovantoji/fullstack_js_dev_nanodegree/blob/main/images/fsjs-c1-l3-before-each-and-after-each.jpg)

![beforeAll_afterAll](https://github.com/leovantoji/fullstack_js_dev_nanodegree/blob/main/images/fsjs-c1-l3-beforeall-and-afterall.jpg)

Skipping or Specifying Tests:
- To skip a test or suite, add `x` in front of `describe` or `it`. This can be helpful to avoid a time-consuming test.
- To focus on one test or suite, add `f` in front of `describe` or `it`. This reduces clutter in the terminal.

The Testing Pyramid
- UI Testing: Does the user interface work as expected?
- End to End Testing: Does the application work as expected?
- Integration Testing: Do services integrate as expected?
- Unit Testing: Does the code run as expected?
![testing_pyramid](https://github.com/leovantoji/fullstack_js_dev_nanodegree/blob/main/images/fsjs-c1-l3-testing-pyramid.jpg)

Jasmine works well with **Unit Testing** and **Integration Testing**. Remember, the difference between Unit Testing and Integration Testing is the use of third-party integration. An example would be function that creates an endpoint. This requires a Unit Test. However, if the use case requires testing of the response from the endpoint and requires a third-party tool to do so, this becomes an integration test. Jasmine can be used for **End-to-End Testing** with a tool call **Selenium** to emulate user interactions. For **UI Testing**, Jasmine is simply not helpful.

How a **server works**:
![server](https://github.com/leovantoji/fullstack_js_dev_nanodegree/blob/main/images/fsjs-c1-l4-how-a-server-works.jpg)

**Common HTTP Requests**:
- **GET**: retrieve data from the server.
- **POST**: send data to the server.
- **DELETE**: remove data from the server.
- **PUT**: replace data on the server.
- **PATCH**: update data on the server.

**Query Parameters**:
- Query strings are parameters in the URL, identified by a `?`.
- To chain multiple parameters together in a query string, use `&`.
![query_string](https://github.com/leovantoji/fullstack_js_dev_nanodegree/blob/main/images/fsjs-c1-l4-query-parameters.jpg)

**HTTP Response Status Codes**:
|Status Code Range|Example Code|
|:-|:-|
|100-199: information|<ul><li>100: Continue</li></ul>|
|200-299: request was successful|<ul><li>200: OK</li><li>201: Created</li></ul>|
|300-399: request was redirected|<ul><li>301: Moved Permanently</li><li>307: Temporary Redirect</li></ul>|
|400-499: client-side error|<ul><li>400: Bad Request</li><li>401: Unauthorized</li><li>405: Method not Allowed</li></ul>|
|500-599: server-side error|<ul><li>500: Internal Server Error</li></ul>|

**Idempotency**: multiple identical requests to the API. The only method not considered idempotent is **POST** since **POST** adds a new resource each time. On the other hand, **GET**, **DELETE**, **PATCH**, and **PUT** act on the same resource each time producing the same result.

|HTTP Request|Idempotency and Security|
|:-|:-|
|**GET**|<ul><li>Safe because the database doesn’t change</li><li>Endpoint is stored in session history</li><li>Can be cached</li><li>Often logged</li></ul>|
|**POST**|<ul><li>Endpoint not stored in session history</li><li>Protects user data from being inadvertently exposed</li></ul>|

The structure of an Express project is very similar to the structure of a book:
- The server acts as the entry point or title page of the book.
- The `package.json` file includes the publisher/copyright information.
- The main route file acts as an index to the different chapters in your book.
- Each route file contains the endpoints for available actions.
![query_string](https://github.com/leovantoji/fullstack_js_dev_nanodegree/blob/main/images/fsjs-l1-c4-express-is-like-a-book.jpg)

**Express Basics**:
- Application Object: every Express application requires the creation of an application object. All of the core functions of Express take place on the application object including endpoint methods. Core methods include:
    - `.listen()`: listens for connections to a specified host and port.
    - `.get()`: used to get a route. This method takes a route and a callback function as arguments. The callback function takes two arguments, the request from the browser and the response from the server. In addition, middleware can also be passed in as an argument.
    - `.post()`, `.put()`, `.delete()`: the other app methods that make up endpoints. They require having the ability to store data.
![server_creation](https://github.com/leovantoji/fullstack_js_dev_nanodegree/blob/main/images/1f2aeba4-fea0-4a29-bbd5-fcfd307faf1d-4-5005-c.jpg)
- Request Object: is the HTTP request to the server. Request has many properties and methods available to it for getting information about the request from the browser.
    - `ip`: a property to get the IP of the request.
    - `cookies`: a property to access cookie information of a request.
    - `path`: a property to get the path of the URL request.
    - `subdomains`: a property to get the subdomain of a URL request.
    - `params()`: a method to get the param values from a request URL.
- Response Object: is returned by the server after a request. It is the response from the server back to the browser.
    - `send()`: a method to send a response from the server to the browser.
    - `status()`: a method to set an HTTP status.
    - `cookie()`: a method to set a cookie for the route.

**Middleware** is a function that is applied between the request and response. Common uses of middleware include checking the authentication status of a user before sending a response or logging the request before sending the response.
![middleware](https://github.com/leovantoji/fullstack_js_dev_nanodegree/blob/main/images/fsjs-c1-l4-middelware.jpg)

Types of middleware:
- Built-in middleware. Express contains 3 built-in middlewares:
    - `express.static`: serving static files (e.g., HTML, etc.)
    - `.json`: parsing incoming JSON
    - `.urlencoded`: parsing incoming urlencoded data
- 3rd-party middleware: installed through NPM.
- Custom middleware.

There are 2 ways to apply middleware:
- Application/route level: Apply the middleware to an entire application or the entirety of a route on either the entry point application object, or to specific routes.
    ```ts
    app.use(middleware);
    ```
- Endpoint level: Apply middleware to specific endpoint.
    ```ts
    students.get('/', middleware, (req, res) => {
        // do something
    });
    ```

**Router Object**:
When building an express application, it is best practice to keep the server and application endpoints and functionality separate. With the router object, you are able to create a directory of routes and separate the functionality of each route onto its own file.

File System is one of the core `node.js` modules. It is a larger module and requires import for use. Working with the file system allows you to access files within your system, and then on the server once the project is launched. It only allows access to the local file system, not users' file systems. The File System Module also allows us to work with data by creating, delete, reading, and writing to files. File System is almost entirely asynchronous by default, but there are some methods that are synchronous and should only be used when first opening a file such as wanting to have a file read before the rest of the code runs. Otherwise, the remainder of the file system module is asynchronous. To avoid using callbacks, we can use the File System Promises API which allows the asynchronous methods to return promises.
```ts
import {promises as fsPromises} from 'fs';
```

**File System vs Database**:
![fs_vs_db](https://github.com/leovantoji/fullstack_js_dev_nanodegree/blob/main/images/fsjs-c1-l4-filesystem-vs-database.jpg)

**File System Flags** are used for identifying read/write operations available when opening a file.
- `r`: allows for the reading of a file.
- `r+`: allows for the reading and writing of a file, will overwrite content in the file.
- `w+`: allows for the reading and writing of a file, will create a file if it does not yet exist.
- `a`: allows for reading and writing of a file and will append new content to the end of the file, not overwriting current content.
- `a+`: allows for reading and writing of a file, will create a file if it does not yet exist, and will append new content to the end of the file, not overwriting current content.

**Write to a file**:
- `.open()`: Used to open a file. Takes a filename and flag as arguments.
    ```js
    const writeData = async () => {
        const myFile = await fsPromises.open('myfile.txt', 'a+');
    }
    ```
- `.write()`: Used to write to a file that is already open. Takes data, and options as arguments.
    ```js
    const writeData = async () => {
        const myFile = await fsPromises.open('myfile.txt', 'a+');
        await myFile.write('TEXT TO BE ADDED');
    }
    ```
- `.writeFile()`: Used to write to a file, overwriting any content that may already exist in the file. Takes a filename, data, and options as arguments.
    ```js
    const writeData = async () => {
        const myFile = await fsPromises.writeFile('myfile.txt', 'TEXT TO BE ADDED')
    }
    ```

**Read, Move, Rename, and Delete files**:
- `.read()`: Used to read a file. The file must be opened first. Allows for reading only a portion of a file, but requires the creation of a buffer to do so. Takes a buffer and options as arguments.
    ```js
    const readData = async () => {
        const buff = new Buffer.alloc(26);
        const myFile = await fsPromises.open('myfile.txt', 'a+');
        await myFile.read(buff, 0, 26);
        console.log(myFile);
    }
    ```
- `.readFile()`: Used to read the entire contents of a file. Takes a path and options as arguments. Is the preferred method for reading files when the entire content needs to be read.
    ```js
    const readData = async () => {
        const myFile = await fsPromises.readFile('myfile.txt', 'utf-8');
        console.log(myFile);
    }
    ```
- `.rename()`: Used to rename or move a file. Takes the old file path and new file path as arguments.
    ```js
    const moveData = async () => {
        await fsPromises.rename('old-name.txt', 'new-name.txt');
    }
    ```
- `.mkdir()`: Used to make new directories. Takes a directory path as an argument.
    ```js
    const makeDir = async () => {
        await fsPromises.mkdir('src');
    }
    ```
- `.unlink()`: Used to remove a file. Takes a file path as an argument.
    ```js
    const removeFile = async () => {
        await fsPromises.unlink('myFile.txt');
    }
    ```
- `.rmdir()`: Used to remove an empty directory. Takes a directory path as an argument.
    ```js
    const removeFile = async () => {
        await fsPromises.rmdir('src');
    }
    ```
