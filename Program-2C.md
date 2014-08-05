## Project: Where In The World Is Tyler Hackbarth?!?

### Part 3: Adding a camera access
#### Due: Thursday by 1:00 p.m.

-----

### Overview

Adding to `signup.html` the ability to take a snapshot using the video camera on your device.

### 1 Copy your code

- Copy your code from Program2B to Program2C.
- Rmemeber the command: `cp -r Program2B Program2C`
- Add a sub-folder to your `Program2C` called `images` and make it writeable by apache:
    - `chmod 777 images`

### 2 Working page:

Below is a working page that accesses the video camera, and binds the "snaphsot" and "save" functionality
to the appropriate buttons. Use the necessary code to incorporate this functionality to your signup form.

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset=utf-8>
	<title>HTML5 Video and Canvas: Video screenshot</title>
	<!--[if IE]><script src="http://html5shiv.googlecode.com/svn/trunk/html5.js"></script><![endif]-->	
	<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js"></script>
	<script>
		// Put event listeners into place
		window.addEventListener("DOMContentLoaded", function() {
			// Grab elements, create settings, etc.
			var canvas = document.getElementById("canvas");
			var	context = canvas.getContext("2d");
			var	video = document.getElementById("video");
			var	videoObj = { "video": true };
			var	errBack = function(error) {
					console.log("Video capture error: ", error.code); 
				};

			// Put video listeners into place
			if(navigator.getUserMedia) { // Standard
				navigator.getUserMedia(videoObj, function(stream) {
					video.src = stream;
					video.play();
				}, errBack);
			} else if(navigator.webkitGetUserMedia) { // WebKit-prefixed
				navigator.webkitGetUserMedia(videoObj, function(stream){
					video.src = window.webkitURL.createObjectURL(stream);
					video.play();
				}, errBack);
			}
			else if(navigator.mozGetUserMedia) { // Firefox-prefixed
				navigator.mozGetUserMedia(videoObj, function(stream){
					video.src = window.URL.createObjectURL(stream);
					video.play();
				}, errBack);
			}
			// Trigger photo take
			document.getElementById("snap").addEventListener("click", function() {
			  //Essentially crops a portion of the video to be our profile pic.
				context.drawImage(video, 100, 100, 400 , 400,0,0,200,200);
			});
			document.getElementById("saveImage").addEventListener("click", function() {
				$.post("backend.php",
				{
					uid : Date.now(),
					name : "test",
					action : "image",
					img : canvas.toDataURL('image/png')
				})
				.done(function(data){
					alert("Data: " + data);
				});
			});
		}, false);
	</script>
</head>
<body>
<video id="video" width="266" height="200" autoplay></video>
<button id="snap">Snap Photo</button>
<canvas id="canvas" width="266" height="200"></canvas>
<button id="saveImage">Save Photo</button>
</body>
</html>
```

### 3 Saving your snapshot:

We have to appropriate javascript to grab a portion of the video, placing it on an html5 canvas. We then bind the save
event to a button to send that "cropped" portion of the video to the server. Our `backend.php` script needs to code to 
handle this "file upload" (essentially).

Add this 'case' to your switch statement:
```php
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
```

[1]: https://cdn1.iconfinder.com/data/icons/UltimateGnome/22x22/status/folder-drag-accept.png "Folder"
[2]: http://www.plcs.net/downloads/images/defaut.gif "File"
