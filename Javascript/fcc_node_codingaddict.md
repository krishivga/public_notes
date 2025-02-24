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
```

## OS module

The OS module provides operating system related utility methods and properties.

```node
os.userInfo() // gives all the user info in an object
os.uptime // outputs the system uptime in seconds (hundreds) as a number
os.type() // outputs the OS name given to node by the operating system
os.release() // outputs OS version
os.totalmem() // outputs total memory
os.freemem() // outputs free memeory
```