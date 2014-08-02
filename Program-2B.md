Not done!!!

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
- Make sure your link in your menu connects to this page. (Remember, we are going to have multiple page site, so we need a menu to link to all of them).
- Take the one from class: `wget http://msu2u.net/Program2/signup.html` or get one from bootsnipp:  http://bootsnipp.com/ and edit as you see fit.
- At this stage, make sure you can add a new user to the database. It should insert a row into your `Users` table, if it doesn't then start checking why.
- Remember, there is no error checking, or handling of passwords. This is the goal of this assignment.

### 3 Adding error checking and password handling

-  I found a nice bootstrap plugin to validate forms here: http://bootstrapvalidator.com/
-  To use, add the following to your pages:

```html
<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/jquery.bootstrapvalidator/0.5.0/css/bootstrapValidator.min.css"/>
<script type="text/javascript" src="//cdnjs.cloudflare.com/ajax/libs/jquery.bootstrapvalidator/0.5.0/js/bootstrapValidator.min.js"></script>
<link rel="stylesheet" href="//cdn.jsdelivr.net/fontawesome/4.1.0/css/font-awesome.min.css" />
```
- There are other ways to use, but for now using hosted libraries is the easiest way.
- Font awesome is included to use the nice icons that accompany the validation.
- To get a feel for how to use this in your form, go here: http://bootstrapvalidator.com/getting-started/#cdn 
- Or here: http://bootstrapvalidator.com/examples/attribute/
- They have some good examples.

### 4 Example form validator

Example Form:

![](http://f.cl.ly/items/1L1v173v0A2G0a0b2g2A/form_validator1_small.png)

Here is the html for the above form. I used a snapshot of the form, because github styles would change the look.
Just place the html in the body of your html page. This method places all of the validation right in the html tags. You can also place the validation in the javascript portion of the validator. 

```html
<form id="attributeForm" method="post" class="form-horizontal"
    data-bv-message="This value is not valid"
    data-bv-feedbackicons-valid="glyphicon glyphicon-ok"
    data-bv-feedbackicons-invalid="glyphicon glyphicon-remove"
    data-bv-feedbackicons-validating="glyphicon glyphicon-refresh">
    <div class="form-group">
        <label class="col-lg-3 control-label">Full name</label>
        <div class="col-lg-4">
            <input type="text" class="form-control" name="firstName" placeholder="First name"
                data-bv-notempty="true"
                data-bv-notempty-message="The first name is required and cannot be empty" />
        </div>
        <div class="col-lg-4">
            <input type="text" class="form-control" name="lastName" placeholder="Last name"
                data-bv-notempty="true"
                data-bv-notempty-message="The last name is required and cannot be empty" />
        </div>
    </div>

    <div class="form-group">
        <label class="col-lg-3 control-label">Username</label>
        <div class="col-lg-5">
            <input type="text" class="form-control" name="username"
                data-bv-message="The username is not valid"

                data-bv-notempty="true"
                data-bv-notempty-message="The username is required and cannot be empty"

                data-bv-regexp="true"
                data-bv-regexp-regexp="^[a-zA-Z0-9_\.]+$"
                data-bv-regexp-message="The username can only consist of alphabetical, number, dot and underscore"

                data-bv-stringlength="true"
                data-bv-stringlength-min="6"
                data-bv-stringlength-max="30"
                data-bv-stringlength-message="The username must be more than 6 and less than 30 characters long"

                data-bv-different="true"
                data-bv-different-field="password"
                data-bv-different-message="The username and password cannot be the same as each other" />
        </div>
    </div>

    <div class="form-group">
        <label class="col-lg-3 control-label">Email address</label>
        <div class="col-lg-5">
            <input class="form-control" name="email" type="email"
                data-bv-emailaddress="true"
                data-bv-emailaddress-message="The input is not a valid email address" />
        </div>
    </div>

    <div class="form-group">
        <label class="col-lg-3 control-label">Password</label>
        <div class="col-lg-5">
            <input type="password" class="form-control" name="password"
                data-bv-notempty="true"
                data-bv-notempty-message="The password is required and cannot be empty"

                data-bv-identical="true"
                data-bv-identical-field="confirmPassword"
                data-bv-identical-message="The password and its confirm are not the same"

                data-bv-different="true"
                data-bv-different-field="username"
                data-bv-different-message="The password cannot be the same as username" />
        </div>
    </div>

    <div class="form-group">
        <label class="col-lg-3 control-label">Retype password</label>
        <div class="col-lg-5">
            <input type="password" class="form-control" name="confirmPassword"
                data-bv-notempty="true"
                data-bv-notempty-message="The confirm password is required and cannot be empty"

                data-bv-identical="true"
                data-bv-identical-field="password"
                data-bv-identical-message="The password and its confirm are not the same"

                data-bv-different="true"
                data-bv-different-field="username"
                data-bv-different-message="The password cannot be the same as username" />
        </div>
    </div>
</form>
```
Then place the following in a script tag:
```js
$(document).ready(function() {
    $('#attributeForm').bootstrapValidator();
});
```

If you wanted to perform your validation in a script tag, then here is a partial example. This assumes that you have a form with the `id` "registration":
```js
		$('#registration').bootstrapValidator({
			container: 'tooltip',
			feedbackIcons: {
				valid: 'glyphicon glyphicon-ok',
				invalid: 'glyphicon glyphicon-remove',
				validating: 'glyphicon glyphicon-refresh'
			},
			fields: {
				firstName: {
					validators: {
						notEmpty: {
							message: 'The first name is required'
						}
					}
				},
				lastName: {
					validators: {
						notEmpty: {
							message: 'The last name is required'
						}
					}
				},
				phone: {
					validators: {
						digits: {
							message: 'The phone number can contain digits only'
						},
						notEmpty: {
							message: 'The phone number is required'
						}
					}
				}
			}
		});
```

Ok, so here is a partially working example (validation) + (form submission): http://msu2u.net/Program2/signup.html
It's jacked up looking, but I was just testing the validation on a couple of fields (using the above javascript). 

You can create an entire new form using the new site, or add validation to the existing form we have been using. For simplicity, I would recommend cut and paste from this site, and make an entire new form. It has all the proper class names and attributes so you won't have to worry about them. 

#### 5 Submitting your form

The snippet below, will submit a form with the `id` "register" to the `url`: "backend.php". If it is succesful, it will pop up an alert with the status (success). 

```js
		$("#register").click(function() {
			console.log($( "#registration" ).serialize());
			$.ajax({
				type: "POST",
				url: "backend.php",
				data: $( "#registration" ).serialize()
			}).done(function( msg ) {
				alert( "Data Saved: " + msg );
			});
		});
```		


#### 5 What your project needs up till now (Monday by Class)

- Program2A is just getting the workspace and backend setup.
- Program2B is actually submitting a user to this backend with error checking.
    - First and Last name must be letters only. MANDATORY
    - Email must be validated. MANDATORY
    - Phone number should be numbers only. Not mandatory
    - Sex - Not mandatory
    - Passwords must match, and be hashed using MD5 when written to the database. MANDATORY

All the code has been given to you. In fact a mostly working example here: http://msu2u.net/Program2/signup.html has nearly all you need.

What it doesn't have:
- All the form validation
- The backend NEEDS:
    - Password column added to the table (if yours doesn't have it).
    - When you insert the password, use the MD5 function to hash it. 

Here is a partial example using the md5 function:

```sql
INSERT INTO SomeTable Values('first','last, MD5('password'));
```

See you monday.

[1]: https://cdn1.iconfinder.com/data/icons/UltimateGnome/22x22/status/folder-drag-accept.png "Folder"
[2]: http://www.plcs.net/downloads/images/defaut.gif "File"
