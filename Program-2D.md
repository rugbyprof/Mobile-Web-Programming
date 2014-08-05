#Not Done!
## Project: Where In The World Is Tyler Hackbarth?!?

### Part 4: Adding everyones location
#### Due: Thursday by 11:00 p.m.

-----

### Overview

Add to `index.html` the ability to log your current location, and send it to a backend server. 

### 1 Copy your code

- Copy your code from Program2C to Program2D.
- Remember the command: 
    - `cp -r Program2C Program2D`
- Add the file: `my_users.json`
    - `chmod 777 my_users.json`
- Add the file: `all_users.json`
    - `chmod 777 all_users.json`

- Your should have the following when done:

- ![1] Program2C
    - ![2] `-rwxrwxrwx all_users.json` `(* all user locations in here)`
    - ![2] `-rwxr-xr-x backend.php`
    - ![2] `-rwxr-xr-x index.html`  `(* new code in here)`
    - ![2] `-rwxr-xr-x geo.js`
    - ![1] `drwxrwxrwx images`
    - ![2] `-rwxr-xr-x login.html`
    - ![2] `-rwxrwxrwx my_users.json` `(* users using my instance here)`
    - ![2] `-rwxr-xr-x signup.html`
    - ![2] `-rwxr-xr-x simple-sidebar.css`

### 2 : `my_users.json`

This file will contain anyone using your code on your server. When the user loads the page, they will put their name 
(or nickname, or username, etc.) in a text box above the map. This "name" will be used to label thier location, so
other users may know who they are.

Your json file should look like this:

```json
{
    "Users": [
        ["name_1","location_1","time_1"],
        ["name_2","location_2","time_2"],
        ...
        ["name_n","location_n","time_n"]
    ]
}
```

Creating a json file is not a bunch of string processing, as you may think! Remember from class, we discussed a couple of methods
of creating / reading json files. The method we will leverage here is a couple of simple php functions: `json_encode` and `json_decode`.

```php
//Grab the current contents of the file in json format, and convert to a php associative array:
$DataArray = json_decode(file_get_contents("my_users.json"));

//Add user to "DataArray"
$DataArray["Users"][] = array($_POST['name'],$_POST['location'],$_POST['time']); 

//Write back contents of array to file in json format:
file_put_contents("my_users.json",json_encode($DataArray));
```

### 2 : `all_users.json`

This file will be in the exact same format as `my_users.json`, except there should be MORE users. To update your 
local copy of `all_users.json` simply run the following command:

```bash
    wget http://msu2u.net/Location/all_users.json
```

from your `Program2D` folder. How do you do this?

```php
    //In your backend.php run this command in the proper case of your switch statement
    exec("wget http://msu2u.net/Location/all_users.json");
```

[1]: https://cdn1.iconfinder.com/data/icons/UltimateGnome/22x22/status/folder-drag-accept.png "Folder"
[2]: http://www.plcs.net/downloads/images/defaut.gif "File"