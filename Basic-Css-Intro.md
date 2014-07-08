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

