## Project: Where In The World Is Tyler Hackbarth?!?

### Part 2: Adding a registration form

### Overview

Adding your signup form to `signup.html`. This form will add a row to the `Users` table in our database, which will then subsequently allow the user to login, and be tracked.


### 1 Create Your Form

- Add a form to `signup.html` 
- Here is an example form: http://bootsnipp.com/snippets/featured/mix-amp-match-register
- Change as appropriate so it has the following fields:

|  Field      | field name  | type           |
|-------------|-------------|----------------|
| First Name  | First       | text           |
| Last Name   | Last        | text           |
| Tumbnail    | Thumb       | file           |
| Sex         | Sex         | radio          |
| Phone       | Phone       | text           |
| Email       | Email       | text           |
| Password    | Pass        | password       |

- This form won't have an action, we will use javascript to submit the form.
- Its submit method will be post: `method=post`

http://msu2u.net/Assignment4/signup.html

