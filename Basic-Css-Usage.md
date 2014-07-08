## Applying CSS

### Divsions

- Divisions are a block level HTML element used to define sections of an HTML file. 
- A division can contain all the parts that make up your website.
- Including additional divisions, spans, images, text and so on.
- The core element used in layouts.
- You define a division within an HTML file by placing the following between the <body></body> tags:

```html
<div id=”container”>
Site contents go here
</div>
```

-----

### Spans

- Spans are very similar to divisions except they are an inline element versus a block level element. 
- No linebreak is created when a span is declared.
- You can use a span tag to style portions of text, as shown in the following:

```html
<span class=”italic”>This text is italic</span>
```

-----

### Margins
#### Inherited: No

- The margin property declares the margin between an HTML element and the elements around it. 
- The margin property can be set for the top, left, right and bottom of an element. 

```css
  margin-top: length percentage or auto; 
  margin-left: length percentage or auto;
  margin-right: length percentage or auto;
  margin-bottom: length percentage or auto;
```

As you can also see in the above example you have 3 choices of values for the margin property

- length
- percentage
- auto

You can also declare all the margins of an element in a single property as follows:

```css
  margin: 10px 10px 10px 10px;
```

If you declare all 4 values in a single declaration, they are ordered as follows:

- top
- right
- bottom
- left

If only one value is declared, it sets the margin on all sides:

```css
  margin: 10px;
```

If you only declare two or three values, the undeclared values are taken from the opposing side:

```css
  margin: 10px 10px; /* 2 values */
  margin: 10px 10px 10px; /* 3 values */
```

- You can also set the margin property to negative values. 
- If you do not declare the margin value of an element, the margin is 0 (zero).

```css
  margin: -10px;
```

Elements like paragraphs have default margins in some browsers, to combat this set the margin to 0 (zero).

```css
p {
  margin: 0;
}
```

> Note: You do not have to add px (pixels) or whatever units you use, if the value is 0 (zero).
