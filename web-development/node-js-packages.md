# NODE JS PACKAGES

## Anatomy of a NodeJS Project

- Each project has a `package.json` file
- Inside the `package.json` file we can define:
  - `name`
  - `description`
  - `version`
  - `license`
  - `scripts` - abstractions over more complex commands, e.g., you can definea script for starting your app
  - `dependencies` - things needed for your project to work
  - `devDependencies` - things other developers will need in order to develop your package, for example, a the testing fraamework you have used.
  - `peerDependencies` - packages that your package needs that your host should have, i.e., the dependies you expect another package to have if someone else is using your package inside that package
  - `types` - where do the types for this package live (if there are any)
- The presence of a `package.json` file elevates a collection of JavaScript files into a **package**.

## JavaScript Modules - Common JS

- By default, NodeJS uses a module system called `CommonJS`
- Each file has an object called `exports` which we can append to
- We can then use an exported function in another file using `require`
- This works as follows:

  ```JavaScript
  // File 1
  exports.myFunction = () => console.log('Hello');

  // File 2
  const myModule = require("<-path-to-file-1->");
  myModule.myFunction();
  ```

- NOTE: `CommonJS` is not the best syntax to use, but it is something you may see in other code etc.

## Native JavaScript Modules

- JavaScript as a language does now support modules
- Browsers are now working to addopt this syntax - you can check if a given browser supports certain syntax on [caniuse.com](https://caniuse.com/).
- Every module can have two different types of export, **named export** and **default export**.
- You can have multiple named exports per module but only one default export
- The `export` declaration is used to export values from a JavaScript module.
- Exported values can then be imported into other programs with the `import` declaration
- After the `export` keyword, you can use `let`, `const`, and `var` declarations, as well as `function` or `class` declarations.
- Note that if the object to export is declared with `const`, they must be imported with the same variable/ function name.
- You can also use the `export { name1, name2 }` syntax to export a list of names declared elsewhere.

### Named Export

- You can export any variables and functions using the following syntax:

  ```JavaScript
  // hello.js
  export const greeting = 'hello';
  export const sayHello = () => console.log(greeting);

  // code.js
  import {greeting, sayHello} from "./hello.js"
  sayHello()
  ```

- This is a named export.

### Default Export

- To use a default export, write code like the following:

  ```JavaScript
  // hello.js
  const sayHello = () => console.log('hello');
  export default sayHello;

  // code.js
  import greeting from "./hello.js"
  greeting()
  ```

- A default export can be imported with any name of your choosing.
- If you want to export more than one thing using a default export, you can create an object containing all of the things you want to export, and export that object. E.g.,
  ```JavaScript
  export default { function1, function2, function3 }
  ```

## Packages

- Node comes with `npm` - stands for 'Node Package Manager'
- You can use `yarn` as an alternative to `npm`
- `npm` enables management of packages in your project by:

  - fetching packages from your package repository ([npmjs.com](https://www.npmjs.com/) by default)

  - creates a **"lock file"** - packages often depend on other packages, which depend on other packages, and so on. Often, some packages will have overlapping dependencies, so to minimise the number of packages we need to install npm figures out which packages are shared and only gets one copy of them, rather than multiple. It then puts this package dependency tree, which it has minimised, into the **lock file** so that if someone else downloads your package, they import the exact same modules as you.

  - places package code in a directory called "node_modules"

  - Note that you should never commit "node_modules" to git.

## Bundling

- Bundling is the process of combining multiple JavaScript files and producing one file
- This makes linking JavaScript to a html file for a website much easier.
