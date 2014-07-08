### HTML

- `Tag` - Used to tag or "mark-up" pieces of text. Once tagged, the text becomes HTML code to be interpreted by a web browser. Tags look like this:
- `Element` - A complete tag, having an opening and a closing .
- `Attribute` - Used to modify the value of the HTML element. Elements will often have multiple attributes.

For now, just understand that a `tag` a piece of code that acts as a label that a web browser interprets, an `element` is a complete `tag` with an opening and closing `tag`, and an `attribute` is a property value that customizes or modifies an HTML element.

Example:
- 'Element` = `<a href="blah">Blah</a>` or an "anchor"
- `Tag` = `<a>`
- `Attribute(s) = `href` & `style`

```html
<a href="http://wwww.google.com" style="color:blue">Google</a>
```

### Mobile What?

- Responsive
- Fluid


### Mobile How?

The following examples are a 

### HTML5 doctype

```html
<!DOCTYPE html>
<html lang="en">
  ...
</html>
```

### Mobile first

Add this to your `head` tag. More about viewports later.
```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

This disables zooming on a mobile device. Not recommended, basically use with caution.
```html
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
```



#### Fonts

```css
font-family:"Times New Roman",Georgia,Serif;
```

