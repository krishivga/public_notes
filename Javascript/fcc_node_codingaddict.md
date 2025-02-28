Starting from modules on this because I'm too lazy to re-write my older notes into a decent format.

# Modules
A module is a seperate file given it's own specific job. This is the alternative to writing all of your code in one big file, as this allows code to be modular- it is reusable and easier to manage.

The contents of a module, to be used elsewhere, first need to be exported. All files are modules by default, and we can access export by using the *module* object.

```node
const variable_one = "xyz";
const function_two = (parameter) => {
    console.log("This is working!");
}

module.exports = {variable_one, function_two};

// For a single export, you may:
module.exports = variable_one;

//You may also export directly from assignment
module.exports.items = {item_1, item_2};

// These all do the same things.
```

In a way, both methods are doing the same thing. In one method, we put the multiple items into an object and export. In the other method, we directly export the item. Either way, only one argument is accepted.

To use a module in another file, you need to *import* it. 

```node
const variable_a = require("./module_name.js");
```

Note on addresses:

"./" represents the current folder

"../" represents the folder above

"/" signfies the next item is a child of the current item

"./module.js" is a file in the same folder

"./folder/module.js" is in a file inside another folder

"../module.js" file is in a folder above.

"../folder/module.js" is inside another folder which is a folder above


Additionally, you may also invoke a file (basically, run it) by simply 'requiring' the file without any exports.

```node
require(`./filename.js`)
```

This will run the file. This is because every time a file is imported, it is run (even if it doesn't have any exports). 

# Built-in Modules

Modules available by default for interacting with the OS and other essential functions. These also require no installation, while external modules do.

You can import modules using just their name.
```node
const variable = require('moduleName')

// You may want to import specific methods of a module
const {methodName, methodName2} = require('moduleName')

// These methods can now be used directly
methodName()

// Instead of 
moduleName.methodName()
```

Note: Path is always in quotes.

## OS module

The OS module provides operating system related utility methods and properties.

You can access methods of a module using `moduleName.method`.

```node
os.userInfo() // gives all the user info in an object
os.uptime // outputs the system uptime in seconds (hundreds) as a number
os.type() // outputs the OS name given to node by the operating system
os.release() // outputs OS version
os.totalmem() // outputs total memory
os.freemem() // outputs free memeory
```

## Path module

Provides utilities for working with file and directory paths.

```node
path.sep // returns the platform specific seperator
path.join(args) // joins path segments using platform specific seperator; returns a normal path
path.basename(path) // provides the name of the file, not the full path (when given a path)
path.resolve(args) // provides absolute path given a filepath.
```

## FS module

Provides utilities to work with the filesystem of a computer.

### Synchronous

When a synchronous fs process is happening, everything else in the server is stopped until that process is complete.

```node
fs.readFileSync(path, encoding) // Reads file specified in path. Encoding must be in '' as well
fs.writeFileSync(file_name, value) // Creates a file with value and given filename. 
```

For `writeFileSync()`, note that the filename must be a path to where the file is stored, ending in the name and file type. E.g. "./folder/folder_2/file.txt". Additionally, if the text file already exists; all existing values will be overwritten.

### Asynchronous 

All asynchronous methods require callback functions. Callbacks follow a **first error convention** where the first argument is always the error and the second argument is the result, like `(error, result) => {}`.

```node
readFile(path, encoding, callback) // Will read file specified in path.
writeFile(path, value, callback) // Will write a file in specified path with given value.
```

Asynchronous methods have the benefit of running in the background- you don't need to stop current system processes to get them to work. Since they run in the background, they have no 'order' of operation and must be nested in each other.

What essentially happens is that when a method like readFile is called, the callback is 'offloaded' to be run in the background and the program can continue like normal.

This is a sample of what a callback for a readFile() function could look like. 

```node
readFile("path",'utf8', (err, result) => {
    if(err) {
        console.log(err)
        return
    }
    // Code block goes here
}
```

If there are multiple asynchronous functions, you will need to nest them. The second function is nested in the first, the third in the second etc.

```node
function_1(path, encoding (err, result) => {
    // code for the first function
    function_2(path, encoding (err, result) => {
        // code for the second function
        function_3(path, encoding (err, result) => {
            // code for the third function
            // and so on
        })
    })
})
```

This is called **callback hell**. The solution is `fs.promises` or async await. 

## HTTP 

Allows admin to setup webserver.

Assume the server is stored on an variable called `server` using `http.createServer`.
```node
http.createServer(callback) - Creates a server
server.listen() - Allows user to accesss server at the specified port.
```
For the createServer callback, we have two arguments; request which is the things we ask to the user and information we recieve, response is what we send to the user and what they recieve. Inside the callback, you can use some methods to do interesting things.

```node
const server = http.createServer((request, response) => { // server is the variable where http.createServer was used.

    // For response

    response.write(text) - Sends a message
    response.end(text) - ends the response

    // For request
    console.log(request) // You can print out the request (once any interaction including a reload happens on the website) to see all info on the object
    request.url - Outputs the current URL the user is on.
    
})
```

To view your node servers locally, you need to use `localhost:xxxx` where *xxxx* are the numbers you entered in the `server.listen()` method.

On all response messages, you can additionally write HTML and CSS directly into the page as formatting. For most messages, you can directly add the message through `response.end` to avoid duplication if a message only has to be sent once. Also, remember that the message is actually an entire webpage.

# NPM

A way to download packages that can significantly reduce development time by using solutions to already solved problems.

A *local dependency* is a pacakge you only want to use for a specific project.

All your important package info goes into *package.json* which is referred to as the manifest file. 
This file also includes all the packages you locally install in this project as dependencies. The packages reside in the folder `node_modules`.

For source control, it is standard to create a `.gitignore` file to ignore all the changes made in node_modules as it isn't relevant to your project. Additionally, if you clone a repository and a package.json file already exists, you only need to do `npm install` to install packages.

## NPM commands
`npm` is the global command for everything related to NPM
`npm --verison` lets you check the version
`npm i packagename` installs a package (you can use either `i` or `install`)
`npm install -g packagename` installs a package globally
`sudo npm install -g packagename` installs a package globally for macos
`npm init` -  Create package.json step by step
`npm init -y` - Create package.json with everything default
`npm install packagename --save-dev` installs a package as a dev dependency (can use `-D` as a shortcut). Dev dependecies are used for testing but not for the final product.
`npm uninstall packagename` - uninstalls a package
The 'nuclear' approach to uninstalling a package is to delete the `node_modules` file and then run `npm install` (after removing the dependencies that you wanted to uninstall) to ensure those dependencies get fully removed. 

## Using Packages
Packages can be imported in the same way that builtin modules are `require('packagename')` but still have to be downloaded via npm first.

Package-lock.json locks the version of the package to the version it was downloaded in. This means that future updates that introduce bugs don't suddenly break our code.

Version numbers are broken into three parts, major_update.minor_update.patch. So, `4.2.11` represents 4th major update, 2nd minor update within that major update and 11th patch for that minor update. 

### Using Scripts
You can use scripts in node.js that allow you to carry out specific syntax/commands (in the script section of package.json).

```node
// Example of script syntax
scripts {
    "start": "node app.js"
}
```
For some scripts, you can use the shortcut such as `npm start` but for most of them, you will have to run `npm run scriptname`.


### Using Nodemon
Allows for dev-tool insights while running servers as well as some options for automation. Nodemon also automatically restarts after any changes.

```node
scripts {
    "dev": "nodemon app.js" // starts program in dev mode
}
```

# Event Loop
Allows Node JS to do non-blocking IO operations - essentially allowing it to do multiple things at the same time without waiting. This is doable because operations are offloaded to the system kernel when possible.

Synchronus - Javascript reads each program line by line. The first line gets executed before the second one etc.
Single threaded - Can only do one action at a time.

**Event loop function**

What event loop does is run all the immediate tasks first (in order) and all the longer, asynchronous tasks (which may take time), it offloads to the system to process. Once all the immediate tasks are done, the asynchronous tasks are 'called back' using callbacks to run them.

For example, if 3 people send requests, A, B and C.

A and C are requests that can be handled immediately, but B is asynchronous and will take a while. 

The event loop will handle A and C while offloading the processing of B to libuv (consider this to just be the 'system'). Once A and C have been handled, B will be 'called back' to the event loop and will be run (after its processing has been done). 