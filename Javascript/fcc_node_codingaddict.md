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
```

To use a module in another file, you need to *import* it. 

```node
const variable_a = require("./module_name.js")
```

Note on addresses:

"./" represents the current folder

"../" represents the folder above

"/" signfies the next item is a child of the current item

"./module.js" is a file in the same folder

"./folder/module.js" is in a file inside another folder

"../module.js" file is in a folder above.

"../folder/module.js" is inside another folder which is a folder above

