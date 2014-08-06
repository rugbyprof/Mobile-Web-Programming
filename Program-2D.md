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
(or nickname, or username, etc.) in a text box above the map. This "name" will be used as a label for their location, so
other users may know who they are.

Your json file should look like this:

```json
{
    "Name1": {
        "location": "33.917504, -98.513889",
        "time": 1407281999
    },
    "Name2": {
        "location": "33.882739, -98.546505",
        "time": 1407281999
    },
    "Name3": {
        "location": "33.858794, -98.515606",
        "time": 1407281999
    },
    "Name4": {
        "location": "33.862500, -98.573627",
        "time": 1407281999
    }
}
```

Creating a json file is not a bunch of string processing, as you may think! Remember from class, we discussed a couple of methods
of creating / reading json files. Lets use a couple of simple php functions to get the job done for us: `json_encode` and `json_decode`.

```php
//Grab the current contents of the file in json format, and convert to a php associative array:
$DataArray = json_decode(file_get_contents("my_users.json"));

//Add user to "DataArray"

//time() is a php function that gets current unix timestamp

//Were using the 'user_name' as an array index, so that every time we add
//that user to the list, it will overwrite the previous entry, and not
//just continuously add another user to the end of the array.

$DataArray[$_POST['user_name']] = array($_POST['user_location'],time()); 

//Write back contents of array to file in json format:
file_put_contents("my_users.json",json_encode($DataArray));
```

One thing you need to make sure of is that your `my_users.json` file starts out with the following in it:

```json
{}
```
or
```json
{

}
```
This basically depicts an empty object. That way, when you open the file and decode the json, you create
an empty php array waiting for values to be added.

### 2 : `all_users.json`

This file will be in the exact same format as `my_users.json`, except there should be MORE users. To update your 
local copy of `all_users.json` simply run the following command:

```bash
    wget http://msu2u.net/Location/all_users.json
```

from your `Program2D` folder. How do you do this in php?

```php
    //In your backend.php run this command in the proper case of your switch statement
    exec("wget http://msu2u.net/Location/all_users.json");
```

### 3 : Add a case to your backend switch statement.

Here is the original backend with the case to handle the json reading and writing:

```php
	switch($_POST['action']){
		
		//Adding a new user into our most splendid spy program
		case "insert":
			fwrite($fp,"inserting\n");
			if(AddUser($db,$fp)){
				$Result = array("Success"=>1);
			}else{
				$Result = array("Success"=>0,"Message"=>"Add user query failed!");
			}
		break;
		
		//Switching a user from either logged in or busy to vice versa.
		case "login":
			if(LoginUser($db)){
				$Result = array("Success"=>1);
			}else{
				$Result = array("Success"=>0,"Message"=>"Login query failed!");
			}
			break;
		
		//Make a user busy.
		case "busy":
			if(BusyUser($db)){
				$Result = array("Success"=>1);
			}else{
				$Result = array("Success"=>0,"Message"=>"Busy user query failed!");
			}
			break;
					
		//Remove a user completely from our spy program
		case "delete":
			if(DeleteUser($db)){
				$Result = array("Success"=>1);
			}else{
				$Result = array("Success"=>0,"Message"=>"Delete query failed!");
			}
			break;
		
		//Getting all logged in users (busy or not)
		case "select":
			$Result = GetLoggedInUsers($db);
			if($Result){
				$Result['Success'] = 1;		//Add success to the result object.
			}else{
				$Result = array("Success"=>0,"Message"=>"Get logged in users query failed!");
			}
			break;
		//Adding a snapshot to the images directory from our mobile camera
		case "image":
			define('UPLOAD_DIR', 'images/');
			$img = $_POST['img'];
			$img = str_replace('data:image/png;base64,', '', $img);
			$img = str_replace(' ', '+', $img);
			$data = base64_decode($img);
			$file = UPLOAD_DIR . $_POST['uid'] . '.png';
			$success = file_put_contents($file, $data);
			$Result =  array("Path"=>$file,"FileSize"=>$success,"Image"=>$_POST['img']);
			break;
		case "update_users":
			if($_POST['user_name']){
				//Grab the current contents of the file in json format, and convert to a php associative array:
				$DataArray = json_decode(file_get_contents("my_users.json"));
				//Add user to "DataArray"
				$DataArray[$_POST['user_name'] = array($_POST['user_location'],time()); 
				//Write back contents of array to file in json format:
				file_put_contents("my_users.json",json_encode($DataArray));
			}
			exec("wget http://msu2u.net/Location/all_users.json");
			break;
		default:
			$Result =  array("Success"=>0,"Message"=>"No action set!");	
	}
```

[1]: https://cdn1.iconfinder.com/data/icons/UltimateGnome/22x22/status/folder-drag-accept.png "Folder"
[2]: http://www.plcs.net/downloads/images/defaut.gif "File"
