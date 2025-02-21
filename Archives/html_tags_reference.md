Self-closing tags do not require a `</xyz>` at the end of the tag. e.g. a non-self closing tag, `<html></html>` while a self-closing tag would be, `<meta>`. These tags are signified as **self-closing** in bold.
`<element property="value">` 
# General Properties
`class` - Gives a tag to an element that allows manipulation of elements as a group (usually in CSS).

`id` - Gives an ID to an element for referencing/CSS manipulation

`aria-label` - Labels elements that accessibility systems may have difficulty understanding.

`aria-labelledby` - Labels elements that cannot be labelled directly for accessibility purposes

`aria-hidden` - Hides an element and it's contents from a screen reader (true/false).

`role="description"`- Role is a part of the Web Accessibility Initiative that provides a description of each element to accessibility tools to help make websites more accessible for disabled people.
# Basics 
`<!-- -->` - Comment line/block

`<html>` - The main tag of the HTML document, all HTML code must be enclosed within it.

`<head>` - Contains metadata about the document.

`<body>`  - Contains all elements of the HTML document (basically all the stuff that is visible)

`<footer>` - Defines a footer for the HTML document
# MetaData
`<link>` - Defines the relationship between the current document and an external resource. 	
- `rel` - Type of document being linked e.g. 'stylesheet'
- `href` - Link to the document e.g. 'styles.css'

`<meta>` - Defines the metadata in a HTML document. Contained within `<head>`. **Self-Closing.**
- `charset` - Specifies the encoding (type of unicode encoding, each unicode number is related to a short phrase or a letter) of the HTML document.
- `name` -  Gives a name to the meta tag.
- `content` - Specifies values associated with name attribute.

# Basic Content
`<main>` - The content in the main tag is unique to that HTML document; unlike metadata and navbars. It is where most of the content in the HTML document goes.

`<h1>`,`<h2>`...`<h6>` - Heading tag to create large text. Becomes smaller in size as the number increases.

`<p>` - Paragraph tag.

`<a>` - Defines a hyperlink.
- `href` - Specifies the destination of the hyperlink.
- `target` - Specifies the type of link/way the link is opened.
	- `_blank` - Allows the link to be opened in a new tab.

`<strong>` - Gives bold effect to enclosed text.

`<code>` - Allows for code to be shown in HTML

`<blockquote>` - Allows for text in quotation blocks
# Images and Media
`<img>` - Displays an image from a referenced location. **Self-closing**.
- `src` - Defines the source for the image
- `alt` - Defines alternative text if the image isn't being displayed
- `rel` - 
- `loading` - Defines how the image is loaded
	- `lazy` - Means that the image won't be loaded until it is needed
- `width` - Defines width for the image (e.g. 400 means 400 pixels)

`<figure>` - Contains self-contained content from the document such as images or documents.
- `<figcaption>` - Adds a caption to the image or figure shown in the tag above.

# Sectioning and Boxes
`<header>` - Provides a place to set the introductory information of a page, usually an image and a h1 tag.

`<nav>` - Defines the main navigation links of a document. Usually put in the `<header>`

`<section>` - Creates a section inside the HTML document.

`<div>` - Used to group sections of a web page into one singular block.

`<span>` - Equivalent of div but on the inline level instead of the block level.

`<article>` - Specifies independent, self contained content. Stuff like blogs and articles.

`<label>` - Increases the 'hit' area for certain types of tags. 
- `for` - Specifies the id of the form element that the label should be bound to
 
`<fieldset>` - Draws a box and groups related elements in a form.

`<legend>` - Provides a caption for fieldset.

`<hr>` - Creates a page break. **Self-closing**

`<aside>` - Defines content visible on the side of the main content (like a sidebar or content describing an image)

# Lists and Tables
`<ul>` creates a bulleted list.
- For each bullet point, the point must be enclosed in the `<li>` list item tag. 

```html
<ul>
	<li> Item 1 </li>
	<li> Item 2 </li>
</ul>
```

`<ol>` creates a ordered (numbered) list.
- For each bullet point, the point must be enclosed in the `<li>` list item tag. Similar to `<ul>` in code structure.

`<table>` - Creates a table
`<caption>` - Provides a caption for the table 
`<thead>` - Used to group the header content of a table
`<tbody>` - Used to group the body content of a table
`<tr>` - Defines a table row
`<td>` - Defines table data 
`<th>` - Defines table headers
`<caption>` - Describes what the table is about. Should always be the first child of the table. 

# Forms
`<form>` - Creates a HTML form for input
- `action` - Tells the form where to send the form data when it is submitted.
- `method` - Decides how information is sent over. Usually either `get` or `post`

`<input>` -  Specifies input field where users can enter data.
- `type` - Specifies the type of input.
- `id` - ID (usually text) that uniquely identifies this form element
- `name` - Specifies name for input element
- `value` - Specifies a value the element gives when selected.
- `placeholder` - Specifies placeholder text to be put inside input element
- `minlength` - defines the minimum length for a input
- `pattern` - Forces use of certain characters or sets of characters only in a password.`pattern="[a-z0-5]{8,}"`, this results in minimum length of 8, a to z allowed and numbers from 0 to 5 allowed

`<button>` - Creates a clickable button.
- `type` - Defines the type of button (values: `button`,`reset` ,`submit`)

`<select>` - Creates a dropdown that contains options. This element contains option elements within it that describe the possible options in the dropdown.

`<option>` - Displays an option in a dropdown.
- `value` - Determines the value that the option sends back to the server when selected

`<textarea>` - Provides the user with an area of text to type long answers in.
- `rows` and `cols` - Increase the vertical and horizontal area of textarea

# Additional Tips
You can group multiple input elements (for example, if you want to only make one radio button selectable out of a set) by giving all of them the same name.

You can link internally by linking the ID of an element in the `href` section of an `<a>` link. e.g. `<a href="#Homepage">Go to Homepage</a>`
