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

> You do not have to add px (pixels) or whatever units you use, if the value is 0 (zero).

-----

### Padding
#### Inherited: No

Padding is the distance between the border of an HTML element and the content within it.

- Most of the rules for margins also apply to padding, except there is no “auto” value.
- Negative values cannot be declared for padding.

```css
padding-top: length percentage; 
padding-left: length percentage;
padding-right: length percentage;
padding-bottom: length percentage;
```

As you can also see in the above example you have 2 choices of values for the padding property

- length
- percentage

You can also declare all the padding of an element in a single property as follows:

```css
padding: 10px 10px 10px 10px;
```

If you declare all 4 values as I have above, the order is as follows:

- top
- right
- bottom
- left

If only one value is declared, it sets the padding on all sides:

```css
padding: 10px;
```

If you only declare two or three values, the undeclared values are taken from the opposing side:

```css
padding: 10px 10px; /* 2 values */
padding: 10px 10px 10px; /* 3 values */
```

> If you do not declare the padding value of an element, the padding is 0 (zero).<br>
You do not have to add px (pixels) or whatever units you use, if the value is 0 (zero).


