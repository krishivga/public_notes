Node JS is used to build server side apps. In contrast to regular JS, node has no DOM and no Windows, as well as no access to browser-side APIs. The benefit though, is filesystem access and responding to network requests (as well as node being based on its own versions rather than browser versions).

*Installed Node LTS via installer*

Two types of ways to 'run' node.js code.
**REPL (Run, Evaluate, Print Loop)**  - Command line mode to run one line of code at a time
**CLI** - Process files for running and debugging.

CLI is what will be used for everything, REPL is only for very niche testing cases.

In almost all cases, you want to use backticks (\`) instead of quotes (") for strings.

## REPL mode
```node
 /* You can start REPL mode with*/
 node
 /* You can exit with */
 .exit
 ```

## Declaration
Node JS allows for declaration and assignment at once. You can create constants using `const`.
```node
const message = "hello world!"
```

## IFs 
```node
if(condition){
	code block
} else {
	code block
}
```

## Functions

```node
// Function creation
const functionName = (parameters) => {
code block
}

// Function usage
functionName(parameters)
```

## Objects
```node
// Object creation
const objectName = {items}

//Object referencing (variables)
objectName.variableName
```
## Output
You can print using `console.log("string")`.

## Executing Node JS
*Via terminal* - `node appname.js`
*Via VSCode* - just use run (ctrl-f5)

## Global Variable
Variables you can access **anywhere** in your applicaation.
`__dirname` - path to current directory
`__filename` - file name
`require` - function to use modules
`module` - info about current module (file)
`process` - info about environment where the program is being executed 

## Modules
Encapsulated code that provides better structure for an application. We only have to import the parts we want to use, and can let the rest of the code not run. Follows modular architecture and segments the code into modular blocks that can be moved around and repurposed.

*Every file in Node.js is a module by default*

Note: The entire module is executed when data from it is imported.
### Exports
Every module has a Exports{} object; anything that is put in the exports object can be used globally by any file in the application.

```node
module.exports = {variable_1, variable_2} // Assigns variable 1 and 2 to the exports object in module

// You can also export just one value directly
module.exports = functionName
```

Remember that every file is a module, so every file has exports object by default.

### Imports
To import these exported variables, we can import through require.
```node
require(`./filepath`)

// You can use this to save the imported variables somewhere
const variables = require(`./variable_filepath`)
```

For internal modules, you **always** start with `./` in the filepath. For modules two or more folders above, you use `../` and for built-in or third party modules, you don't add anything.

