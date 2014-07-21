## Quiz 2

### Read The Following

- https://developers.google.com/web/fundamentals/layouts/

Which links to the following:

- https://developers.google.com/web/fundamentals/layouts/rwd-fundamentals/
- https://developers.google.com/web/fundamentals/layouts/rwd-patterns/
- https://developers.google.com/web/fundamentals/layouts/navigation-patterns/

### Quiz

There will be a project based, open web, quiz using the concepts learned from the readings.

### Motivation

We will continue to develop our mobile bus app, but take a break tonight (Wednesday) and tomorrow (Thursday) 
to actually study the necessary mobile principles needed to achieve our goal. Basically, we have a working 
template but we want to make sure it includes:
- fluid design
- responsive layout
- incorporation of mobile design patterns

In fact, the more I look at https://developers.google.com/web/fundamentals/ the more I like it. You should look
around the site.

### Actual Quiz Questions

- Name every file exactly as directed!
- Create a folder on your server called: `Quiz2` in your `/var/www/html` directory.
- Use wget to pull the example page from http://msu2u.net/Quiz2 to your server.
    - `wget http://msu2u.net/Quiz2/content.html`
- Also grab the style sheet and background image:
    - `wget http://msu2u.net/Quiz2/vpdemo.css`
    - `wget http://msu2u.net/Quiz2/checker.png`
- Don't edit `content.html` directly, copy it to `one.html`. 
- The changes build from one question to the next, so copy `one.html` to `two.html` and so on.

1. Set the viewport in `content.html` as suggested by our friends at [Google Dev](https://developers.google.com/web/fundamentals/layouts/rwd-fundamentals/set-the-viewport) and save your result in `one.html`
2. Using the suggestions at [responsive web design basics](https://developers.google.com/web/fundamentals/layouts/rwd-fundamentals/) optimize the content from `one.html` for reading, and save it in `two.html`
3. Media Queries.
    - Copy `two.html` to `three.html`
    - Query 1
        - Place an `<h4></h4>` tag right below the `<article>` tag in your code with the following content in it: ` &gt size &gt `. 
        - It should look like: `< size < ` 
        - Now place media queries in your style sheet so that it displays the screen size in your `h4` tag similar to the following: `1000px < size < 900px`.
        - It should change every 100px until the tag contains: `500px < size < 600px`.
   - Query 2
        - Add a 1px white border with rounded corners to h1 and h2 tags when the screen width less than 600 pixels.
   - Query 3
       - Change the font of all lists on the page to be some thick scripted font (found here: https://www.google.com/fonts) when the screen size is between 800 and 1000 pixels. 
   - Query 4
       - Change the background color of the page to white, and the text to black when the screen is less than 500 pixels wide.  

4. When completed you should have a folder that contains (alphabetically):
- ![1] Quiz2
    - ![2] checker.png
    - ![2] content.html
    - ![2] one.html
    - ![2] three.html
    - ![2] two.html
    - ![2] vpdemo.css

[1]: https://cdn1.iconfinder.com/data/icons/UltimateGnome/22x22/status/folder-drag-accept.png "Folder"
[2]: http://www.plcs.net/downloads/images/defaut.gif "File"
