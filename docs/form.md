[Home](index)

# Populating form elements with JQuery View Engine

**[JOVN](https://github.com/JocaPC/jquery-view-engine)** is a simple view engine that enables you to easily populate elements of a HTML form using data in JavaScript objects (models). It is ideal solution for populating HTML forms dynamicaly from an AJAX call.

Let's imagine that you have an empty HTML form in your page:
```html
<form id="companyForm" method="post">

    <input name="Name" type="text"/>

    <textarea name="Address" rows="3" cols="10"></textarea>

</form>
```
And you have a JavaScript model object fetched from some REST API:
```javascript
var model = {
    Name:"Emkay Entertainments",
    Address:"Nobel House, Regent Center"
};
```
In order to bind the object **model** to the form with id **#companyForm**, you need a **single line of code**:
```javascript
$("#companyForm").view(model);
```

The only prerequisite is to include [jquery](https://jquery.com/) and [JOVN](https://github.com/JocaPC/jquery-view-engine/blob/master/src/jquery.view-engine.js) libraries in your page.

**[JOVN](../README.md)** has a **view()** function that can be applied on an empty HTML fragment that represents a template. This function gets the JavaScript object that should be loaded into the template form. **[JOVN](../README.md)** will automatically match the properties in the JavaScript object (*Name* and *Address* in this example) to the form elements by **id** or **name** attributes.

# Complex example

In this example, we will load more complex form with input, textarea, select list, and radio button elements. We will load two objects into this form:
 - One array that represents a list of options that will be dynamically populated into *#Region* select list, 
 - One object that will be loaded into elements of the form. 

First, we need to put a plain HTML code in a HTML page that represents an empty form that we want to show:

```html
<form id="companyForm" method="post">
    <input type="hidden" name="ID"></input>

    <label for="Name">Name</label>
        <input name="Name" type="text"/>

    <label for="Address">Address</label>
        <textarea name="Address" rows="3" cols="10"></textarea>

    <label for="Region">Region</label>
        <select name="Region" id="Region">
    </select>

    <label class="radio-inline">
        <input name="Active" type="radio" value="Active"/>Active
    </label>
</form>
```

This template is a pure HTML form without any custom attributes or placeholders. Any HTML/CSS designer can modify this code without any problem.
Every element in the HTML form has a `name` (or `id`) attribute. **JOVN** use this convention 
 to populate elements in the form.

Now, we need JavaScript objects that will be populated into the SELECT list and FORM:

```javascript
// Options for #Region SELECT list:
var regions = ["North","West","South","East"]);
var company = {
    ID:17,
    Name:"Emkay Entertainments",
    Address:"Nobel House, Regent Center",
    Town:"Lothian",
    Region:"East",
    Active: true
};
```

The following JavaScript code can fill the form above:

```javascript
// Fill options in #Region SELECT list:
$("#Region").view(regions);

// Fill form with data in the model object:
$("form#companyForm").view(company);
```

Some elements such as `SELECT` might have options that are statically embeded in HTML, while others need to be dynamically populated. In the example above, Region list is initially empty, and we can use it as a template and populate it using `$("#Region").view(["North","West","South","East"])`. This code will fill the select list with the four values in the array. 

When we apply a view() function on a template and provide an object that should be bound as an argument, **JOVN** will go through the properties of the object, find the matching elements in the form, and populate them.

**JOVN** will analyze each type of the input and decide how to populate it (for example it will set the value of text inputs, check the checkboxes, select options in the lists or radio buttons by name.) This way, the common logic that we use to manually populate elements depending on a type is built-in into the view engine.

# HTML5 Elements

**JOVN** supports a variety of HTML5 elements such as range, datetime, etc.
See live demo of the complex form with different HTML5 elements that is populated using **JOVN** view engine in [this example](examples/edit.html).

[Home](index)