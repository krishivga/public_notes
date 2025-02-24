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

# HTTP 
