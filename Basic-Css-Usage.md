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
##### Inherited: No

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
##### Inherited: No

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

-----

### Text Properties
##### Inherited: Yes

#### Color

You can set the color of text with the following:
```css
  color: value;
```

Possible values are

- color name – example:(red, black…)
- hexadecimal number – example:(#ff0000, #000000)
- RGB color code – example:(rgb(255, 0, 0), rgb(0, 0, 0))

#### Text Align
You can align text with the following:
```css
  text-align: value;
```

Possible values are

- left
- right
- center
- justify
- Examples:

#### Text Decoration
You can decorate text with the following:

```css
  text-decoration: value;
```

Possible values are

- none
- underline
- overline
- line through
- blink

#### Text Indent
You can indent the first line of text in an (X)HTML element with the following:
```css
  text-indent: value;
```

Possible values are

- length
- percentage

### Text Transform
You can control the size of letters in an (X)HTML element with the following:

```css
  text-transform: value;
```

Possible values are:

- none
- capitalize
- lowercase
- uppercase

#### White Space
You can control the whitespace in anHTML element with the following:
```css
  white-space: value;
```

Possible values are:

- normal
- pre
- nowrap

-----

### Font Properties
##### Inherited: Yes

#### Font
The font property can set the style, weight, variant, size, line height and font:

```css
  font: italic bold normal small/1.4em Verdana, sans-serif;
```

The above would set the text of an element to an italic style a bold weight a normal variant a relative size a line height of 1.4em and the font to Verdana or another sans-serif typeface.


#### Font-Family
You can set what font will be displayed in an element with the font-family property.

There are 2 choices for values:

- family-name
- generic family

If you set a family name it is best to also add the generic family at the end. As this is a priortized list. So if the user does not have the specified font name it will use the same generic family. (see below)

```css
  font-family: Verdana, sans-serif;
```

#### Font Size
You can set the size of the text used in an element by using the font-size property.
```css
  font-size: value;
```

There are a lot of choices for values:

|          |         |           |          |         |          |         |           |          |         |
|----------|---------|-----------|----------|---------|----------|---------|-----------|----------|---------|
| xx-large | x-large | larger    | large    | medium  | small    | smaller | x-small   | xx-small | length  |

#### % (percent)

There is quite a bit to learn about font sizes with CSS so, I am not even going to try to explain it. Actually there are already some great resources on how to size your text. (see below)

What size text should I use in my css by Paul O’B
Dive into accessibility – Font Sizes

Font Style
You can set the style of text in a element with the font-style property

  font-style: value;

Possible values are

normal
itailc
oblique

Font Variant
You can set the variant of text within an element with the font-variant property

  font-variant: value;

Possible values are

normal
small-caps

Font Weight
You can control the weight of text in an element with the font-weight property:

  font-weight: value;

Possible values are

lighter
normal
100
200
300
400
500
600
700
800
900
bold
bolder
