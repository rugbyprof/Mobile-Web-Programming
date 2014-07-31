## Project: Where In The World Is Tyler Hackbarth?!?

### Part 2: Adding a registration form
#### Due: Monday Aug 4th by 1:00 p.m.

-----

### Overview

Adding your signup form to `signup.html`. This form will add a row to the `Users` table in our database, which will then subsequently allow the user to login, and be tracked.


### 1 Copy your code

- Copy your code from Program2A to Program2B.
- Since were doing this in stages, I need to grade each stage individually.
- Simply run this command: `cp -r Program2A Program2B`
- Your should have the following when done:

- ![1] Program2B
    - ![2] backend.php
    - ![2] index.html
    - ![2] geo.js
    - ![2] login.html
    - ![2] signup.html
    - ![2] simple-sidebar.css

### 2 Add an actual form to your signup page

- Add a form to `signup.html`
- Take the one from class: `wget http://msu2u.net/Assignment4/signup.html` or get one from bootsnipp:  http://bootsnipp.com/ and edit as you see fit
- At this stage, make sure you can add a new user to the database. It should insert a row into your `Users` table, if it doesn't then start checking why.
- Remember, there is no error checking, or handling of passwords. This is the goal of this assignment.

### 3 Adding error checking and password handling

- This form won't have an action, we will use javascript to submit the form.
- Its submit method will be post: `method=post`




[1]: https://cdn1.iconfinder.com/data/icons/UltimateGnome/22x22/status/folder-drag-accept.png "Folder"
[2]: http://www.plcs.net/downloads/images/defaut.gif "File"
