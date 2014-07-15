## Program 1 - First Mobile Web Page.
#### Due: July 16th by 1300 hours.
-----

## Bus Stop Logger

This mobile page will consist of a google map displaying your current location. Later we will
animate this process, continuously updating the center of the map to correspond with your location,
but for now simply put your current lat lon in the `textbox` below the map. 

### Starter Code:

Go look at this gist: https://gist.github.com/rugbyprof/54f43596aee4432fe959 to get a copy of [`geo.js`](https://gist.github.com/rugbyprof/54f43596aee4432fe959 )

You can use `wget http://msu2u.net/GMaps1/index.html` to grab a current copy of the index file we worked on in class. I added a bootstrap theme to make it look better.

### Assignment:

- Make sure you have an index file that replicates what we did in class. Grab it using wget from above, or use your own copy, or simply go to the page, and view the source code.  
- Add the `geo.js` file to your folder. 
    - Add a script tag to include `geo.js` in your `index.html`
    - Update `geo.js` so that it writes the devices current Lat/Lon to the textbox below the map.
- Ensure that a button tap places a marker on the map at your current location

### Make Sure

I should be able to browse to: `111.222.333.444/GMaps1` (replacing 111.222.333.444 with YOUR IP address) and view your project. If your path is different, then I won't grade it. 

### Backend Script (extra credit):

In your project folder (GMaps1):
- Create a file called `backend.php` (`chmod 755`)
- Create two files (`chmod 777` on both):
    - `log.txt` used for debugging
    - `bus_stops.txt` used to hold bus stops


```php
<?php

//If data is in the posted array
if($_POST){
	//Pull data out of $_POST
	//Good for readability, not necessary
	$Append = $_POST['append'];
	$Points = $_POST['points'];

	//Init my debug array
	$debug = array();

	//If Append is true, make file open method append
	//otherwise, erase everything.
	if($Append == 'true'){
		$type="a";
		$debug['open_type'] = 'a';
	}else{
		$type="w";
		$debug['open_type'] = 'w';
	}

	//Used for debugging
	//Create a file called log.txt and chmod it to 777
	$debug['points'] = $_POST['points'];
	$debug['time'] = time();
	file_put_contents("log.txt",print_r($debug,true));

	//Open file as specifed (append, overwrite)
	//Make sure bus_stops.txt is 777
	$fp = fopen("bus_stops.txt",$type);

	//Write data to file.
	fwrite($fp,$Points."\n");

	//Return something that lets front end know if things worked. 
	//I just returned true, no matter what for now.
	header('Content-Type: application/json');
	echo '{"success":true}';
}
```
- Grab my `index.html` file, or just look at it to see how I posted the data to the server. 
