### Intro to CSS
A `CSS` (cascading style sheet) file allows you to separate your web sites HTML content from it’s style. 
As always you use your HTML file to arrange the content, but all of the presentation (fonts, colors, 
background, borders, text formatting, link effects & so on…) are accomplished within a CSS.

There are 3 methods for applying style to your pages:

### Inline Style
These kind of defeat the purpose of "cascading style" ... well maybe not?

```html
<p style=”color: #ff0000;”>Some red text</p>
```

### Internal Stylesheet
Simply placing the CSS code within the `<head></head>` section of your page and in between a `<style>` tag.

```html
<head>
<title><title>
<style type=”text/css”>
    <!-- CSS Content Goes Here -->
</style>
</head>
<body>
```

### External Stylesheet
A CSS file contains no HTML, only CSS. You simply save it with the .css file extension. You can link to the file 
externally by placing one of the following links in the head section of every HTML file you want to style with the CSS file.

```html
<head>
<title><title>
<link rel=”stylesheet” type=”text/css”href=”style.css”>
</head>
<body>
```

By using an external style sheet, all of your HTML files link to one CSS file in order to style the pages. 
This means, that if you need to alter the design of all your pages, you only need to edit one .css file to make 
global changes to your entire website.


### Cascading Order

Style is applied in the following order:

1. Inline Style (inside HTML element)
2. Internal Style Sheet (inside the `<head>` tag)
3. External Style Sheet

As far as which way is better, it depends on what you want to do. If you have only one file to style then placing it 
within the `<head></head>` tags (internal) will work fine. Though if you are planning on styling multiple files then the
external file method is the way to go. Inline is probably never good, unless your lazy like me....

-----

### CSS Syntax
The syntax for CSS is different than that of HTML markup. Though it is not too confusing, once you take a look at it. It consists of only 3 parts.

```css
selector { property: value }
```

The selector is the HTML element that you want to style. The property is the actual property title, and the value is the style you apply to that property.

Each selector can have multiple properties, and each property within that selector can have independent values. The property and value are separated with a colon and contained within curly brackets. Multiple properties are separated by a semi colon. Multiple values within a property are sperated by commas, and if an individual value contains more than one word you surround it with quotation marks. As shown below. Indentation is optional, and white space doesn't matter.

```css
body {
  background: #eeeeee;
  font-family: “Trebuchet MS”, Verdana, Arial, serif;
}
```

### Inheritance
When you nest one element inside another, the nested element will inherit the properties assigned to the containing element. Unless you modify the inner elements values independently.

For example, a font declared in the body will be inherited by all text in the file no matter the containing element, unless you declare another font for a specific nested element.

```css
body {font-family: Verdana, serif;}
```

Now all text within the HTML file will be set to Verdana.

If you wanted to style certain text with another font, like an h1 or a paragraph then you could do the following.

```css
h1 {font-family: Georgia, sans-serif;}
p {font-family: Tahoma, serif;}
```

Now all `<h1>` tags within the file will be set to Georgia and all `<p>` tags are set to `Tahoma`, leaving text within other elements unchanged from the body declaration of `Verdana`.

There are instances where nested elements do not inherit the containing elements properties.

For example, if the body margin is set to 20 pixels, the other elements within the file will not inherit the body margin by default.

```
body {margin: 20px;}
```

### Combining Selectors
You can combine elements within one selector in the following fashion.

```css
h1, h2, h3, h4, h5, h6 {
  color: #009900;
  font-family: Georgia, sans-serif;
}
```

As you can see in the above code, I have grouped all the header elements into one selector. Each one is separated by a comma. The final result of the above code sets all headers to green and to the specified font. If the user does not have the first font I declared it will go to another sans-serif font the user has installed on their computer.


### Comment tags
Comments can be used to explain why you added certain selectors within your css file. So as to help others who may see your file, or to help you remember what you we’re thinking at a later date. You can add comments that will be ignored by browsers in the following manner.

```css
/* This is a comment */
body{
   margin:0px;
   background-color:#C0C0C0;
}
```

-----

