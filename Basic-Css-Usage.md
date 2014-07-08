-----

### Applying CSS

### Divsions
Divisions are a block level HTML element used to define sections of an (X)HTML file. A division can contain all the parts that make up your website. Including additional divisions, spans, images, text and so on.

You define a division within an (X)HTML file by placing the following between the <body></body> tags:

<div>
Site contents go here
</div>

Though most likely you will want to add some style to it. You can do that in the following fashion:

<div id=”container”>
Site contents go here
</div>

The CSS file contains this:

#container{
  width: 70%;
  margin: auto;
  padding: 20px;
  border: 1px solid #666;
  background: #ffffff;
}

Now everything within that division will be styled by the “container” style rule, I defined within my CSS file. A division creates a linebreak by default. You can use both classes and IDs with a division tag to style sections of your website.

