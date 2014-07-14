### Geo Location API

Original Article: http://www.html5rocks.com/en/tutorials/device/orientation/

### Introduction

Many new computers, mobile phones and other devices are now shipping standard with `accelerometers`, `gyroscopes`, `compasses` and other hardware designed to determine capture motion and orientation data. At the same time, web browsers are providing increasingly more access to that new hardware. One example of that are the new HTML5 DeviceOrientation and DeviceMotion events. These events provide developers with information about the orientation, motion and acceleration of the device.

Today, all modern mobile browsers support device orientation, and most support device motion, with Chrome for Android and Opera being the holdouts. Thankfully they're working on it and we should see it soon. Note, if you need to support older versions of Firefox, it has an implementation using a slightly different event model.

These events have a lot of fun uses, such as using orientation to control the direction of character in a game, or motion to determine how high a character should jump. Additionally, you can use these events beyond gaming. When used with GeoLocation, you can create a more accurate turn-by-turn navigation system.

In this article, we’ll take a look at the two different events, and use CSS to rotate an image based on the orientation of the device.

### Which end is up?

There are a couple of things that we need to make sure we understand before we can start using these events, which end is up and what are the axes we’re going to use?

### Device Orientation Data

To answer this question, we need to align our device with the local earth frame. To do that, take your device, and put it on flat, level surface with the top of the device pointing directly north. To do this with a phone, turn around until you are facing north, and place the phone on a flat table, with the bottom of the phone closest to you and the top pointed north. For a laptop, the situation is similar, except the screen is open at a 90° angle, facing you and the keyboard in-line with the surface.

| ![Axes](http://f.cl.ly/items/2P2M3L2l2f1t1B0Z3A16/axes.png) |
|-------------------------------------------------------------|
| Phone is in its normal position, on a flat on a surface, with the screen facing up, the top of the phone pointed directly north and the bottom of the phone is closest to you. The `X`, `Y` and `Z` values increase as you move to the right, forward or up respectively. |

### Device Motion Data

Acceleration data is returned as a coordinate frame with three axes, `x`, `y` and `z`. 

- `x-axis` runs side-to-side across the mobile phone screen, or the laptop keyboard and is positive towards the right side. 
- `y-axis` runs front-to-back across the mobile phone screen or the laptop keyboard and is positive towards as it moves away from you. 
- `z-axis` comes straight up out of the mobile phone screen or the laptop keyboard and is positive as it moves up.

| ![Axes](http://f.cl.ly/items/0t2c1Y2v2k3o342L0T38/rotation.png) |
|----------------------------------------------------------|
| The phone is rotated on the `Y-Axis` by `gamma` degrees. |

The rotation data uses Euler angles to represent the difference between the device in it’s normal position and it’s current position. With the HTML5 device orientation events, the data is returned as the number of degrees different from normal. An easier way to think about it is how much the device is tilted `front-to-back`, is referred to as `beta`. How much its tilted `side-to-side`, is known as `gamma`. And finally how much has it been rotated around the `z-axis`, is known as `alpha`.

One thing to keep in mind is that most people don’t use their phones when they’re in this flat position, and instead have rotated them around the `x-axis` so the screen is facing them, this will affect the acceleration data that is returned from the device motion events.

### Differences in Browsers

As mentioned earlier, `alpha`, `beta` and `gamma` are determined based on the position the device is with the local earth frame. For most browsers, `alpha` returns the compass heading, so when the device is pointed north, `alpha` is zero. With Mobile Safari, `alpha` is based on the direction the device was pointing when device orientation was first requested. The compass heading is available in the `webkitCompassHeading` parameter.

## The events

### Device orientation

The device orientation event returns only the rotation data, which includes how much the device is leaning `front-to-back (beta)`, `side-to-side (gamma)` and if the phone or laptop has a compass, the direction the device is facing (`alpha`).

#### Let’s see a couple examples:

| ![](http://f.cl.ly/items/2S1G1w1m1U2s061P3u3U/dm1.png) |
|:--------------------------------------------:|
| You are looking down at a phone that is lying on a flat, horizontal surface, with north at the top of the frame. |
|`{evt.alpha: 0, evt.beta: 0, evt.gamma: 0}` |

| ![](http://f.cl.ly/items/1r2q1A0k0M1a433J1F1i/dm2.png) |
|:--------------------------------------------:|
| You are looking down at a phone that is lying on a flat, horizontal surface, with north at the top of the frame. The phone has been rotated by 180° so it is pointing south.|
| `{evt.alpha: 180, evt.beta: 0, evt.gamma: 0}` |

| ![](http://f.cl.ly/items/0r362Q333o0F1I0I0M1E/dm3.png) |
|:--------------------------------------------:|
| You are looking down at a device that does not have a compass built in, it is pointed west and tilted up by 45° with the left side of the phone higer than the right.|
| `{evt.alpha: null, evt.beta: 0, evt.gamma: 45}` |

| ![](http://f.cl.ly/items/2Z0n1A01342u2j3S3p3W/dm4.png) |
|:--------------------------------------------:|
| You are looking down at a phone that is pointed north and tilted up by 45° with the top of the phone higer than the bottom. |
`{evt.al

### Device motion

The device motion event is a superset of the device orientation event; it returns data about the rotation information and also [acceleration](http://en.wikipedia.org/wiki/Acceleration) information about the device. The acceleration data is returned in three axes: `x`, `y` and `z`. They are measured in [`meters per second squared (m/s^2)`](http://en.wikipedia.org/wiki/Metre_per_second_per_second). Because some devices might not have the hardware to exclude the effect of gravity, the event returns two properties, `accelerationIncludingGravity` and `acceleration`, which excludes the effects of gravity, (when this is the case, the acceleration data will be null).

A laptop in its normal position, with the screen facing up, the data returned would be:

|   | Not accelerating	| Accelerating up	| Accelerating forward	| Accelerating right	| Accelerating up & to the right |
|---|------------------|-----------------|----------------------|--------------------|--------------------------------|
| acceleration |	{0, 0, 0} |	{0, 0, 5} | {0, 2, 0} | {3, 0, 0} | {5, 0, 5}
accelerationIncludingGravity | 0, 0, 9.81} | {0, 0, 14.81} | {0, 2, 9.81} | {3, 0, 9.81} | {5, 0, 14.81}

A mobile phone rotated along the x-axis so the screen is perpendicular to it’s normal position would return:

|   | Not accelerating	| Accelerating up	| Accelerating forward	| Accelerating right	| Accelerating up & to the right |
|---|------------------|-----------------|----------------------|--------------------|--------------------------------|
| acceleration	|	{0, 0, 0}	|	{0, 5, 0}	|	{0, 0, 2}	|	{3, 0, 0}	|	{5, 5, 0} |
| accelerationIncludingGravity	|	{0, 9.81, 0}	|	{0, 14.81, 0}	|	{0, 9.81, 2}	|	{3, 9.81, 0}	|	{5, 14.81, 0} |

## Using the DeviceOrientation events

### 1. Check for compatibility

Check to see if DeviceOrientationEvent supported.
```javascript
if (window.DeviceOrientationEvent) {
 console.log("DeviceOrientation is supported");
}
```
One thing to note, some devices (for example, the original iPad) say that they support the event when in fact they don’t. In these cases, the event is fired only once, and all of the properties are null.

### 2. Declare the markup

For this example, we’re going to display the orientation data and then apply that information as a CSS3 transform to an image.
```html
<div class="main">
  <h2>Device Orientation</h2>
  <table>
    <tr>
      <td>Event Supported</td>
      <td id="doEvent"></td>
    </tr>
    <tr>
      <td>Tilt Left/Right [gamma]</td>
      <td id="doTiltLR"></td>
    </tr>
    <tr>
      <td>Tilt Front/Back [beta]</td>
      <td id="doTiltFB"></td>
    </tr>
    <tr>
      <td>Direction [alpha]</td>
      <td id="doDirection"></td>
    </tr>
   </table>
</div>

<div class="container" style="perspective: 300;">
  <img src="html5_logo.png" id="imgLogo" class="logo">
</div>
```
### 3. Add an event listener

Now that we know what events are supported, add the appropriate event listeners:

if (window.DeviceOrientationEvent) {
  // Listen for the event and handle DeviceOrientationEvent object
  window.addEventListener('deviceorientation', devOrientHandler, false);
}
4. Handle the event

The HTML5 DeviceOrientation event returns three pieces of data:

alpha the direction the device is facing according to the compass
beta the angle in degrees the device is tilted front-to-back
gamma the angle in degrees the device is tilted left-to-right.
The angles values increase as you tilt the device to the right or towards you.
if (window.DeviceOrientationEvent) {
  document.getElementById("doEvent").innerHTML = "DeviceOrientation";
  // Listen for the deviceorientation event and handle the raw data
  window.addEventListener('deviceorientation', function(eventData) {
    // gamma is the left-to-right tilt in degrees, where right is positive
    var tiltLR = eventData.gamma;

    // beta is the front-to-back tilt in degrees, where front is positive
    var tiltFB = eventData.beta;

    // alpha is the compass direction the device is facing in degrees
    var dir = eventData.alpha

    // call our orientation event handler
    deviceOrientationHandler(tiltLR, tiltFB, dir);
  }, false);
} else {
  document.getElementById("doEvent").innerHTML = "Not supported."
}
5. Respond to the data

We’ll display it in the table we created in step 2, and also add rotate the image using a CSS3 transform.

document.getElementById("doTiltLR").innerHTML = Math.round(tiltLR);
document.getElementById("doTiltFB").innerHTML = Math.round(tiltFB);
document.getElementById("doDirection").innerHTML = Math.round(dir);

// Apply the transform to the image
var logo = document.getElementById("imgLogo");
logo.style.webkitTransform =
  "rotate("+ tiltLR +"deg) rotate3d(1,0,0, "+ (tiltFB*-1)+"deg)";
logo.style.MozTransform = "rotate("+ tiltLR +"deg)";
logo.style.transform =
  "rotate("+ tiltLR +"deg) rotate3d(1,0,0, "+ (tiltFB*-1)+"deg)";
The final product


Try it out, and view the source to see it in action.

Using the DeviceMotion events

The DeviceMotionEvent provides the acceleration and rotation data of the device. In our example, we’re going to use accelerationIncludingGravity to determine the orientation of the device and get a similar result to the sample we built with DeviceOrientation.

1. Check for compatibility

First thing we want to do is determine if the DeviceMotionEvent is supported using feature detection.

if (window.DeviceMotionEvent) {
  console.log("DeviceMotionEvent supported");
} 
Like DeviceOrientationEvent, if a browser cannot provide motion information, the event will be fired once and all properties will be null.

2. Add an event listener

Now that we know that the browser and device supports the DeviceMotionEvent, we can add an event listener.

if ((window.DeviceMotionEvent) {
  window.addEventListener('devicemotion', deviceMotionHandler, false);
} else {
  document.getElementById("dmEvent").innerHTML = "Not supported."
}
3. Declare the markup

For this example, we’re just going to display data that we receive.

<div class="main">
  <h2>Device Motion</h2>
  <table>
    <tr>
      <td>Event Supported</td>
      <td id="dmEvent"></td>
    </tr>
    <tr>
      <td>acceleration</td>
      <td id="moAccel"></td>
    </tr>
    <tr>
      <td>accelerationIncludingGravity</td>
      <td id="moAccelGrav"></td>
    </tr>
    <tr>
      <td>rotationRate</td>
      <td id="moRotation"></td>
    </tr>
    <tr>
      <td>interval</td>
      <td id="moInterval"></td>
    </tr>
  </table>
</div>
4. Create an event handler

We want to display the raw data that we get back.

function deviceMotionHandler(eventData) {
  var info, xyz = "[X, Y, Z]";

  // Grab the acceleration from the results
  var acceleration = eventData.acceleration;
  info = xyz.replace("X", acceleration.x);
  info = info.replace("Y", acceleration.y);
  info = info.replace("Z", acceleration.z);
  document.getElementById("moAccel").innerHTML = info;

  // Grab the acceleration including gravity from the results
  acceleration = eventData.accelerationIncludingGravity;
  info = xyz.replace("X", acceleration.x);
  info = info.replace("Y", acceleration.y);
  info = info.replace("Z", acceleration.z);
  document.getElementById("moAccelGrav").innerHTML = info;

  // Grab the rotation rate from the results
  var rotation = eventData.rotationRate;
  info = xyz.replace("X", rotation.alpha);
  info = info.replace("Y", rotation.beta);
  info = info.replace("Z", rotation.gamma);
  document.getElementById("moRotation").innerHTML = info;

  // // Grab the refresh interval from the results
  info = eventData.interval;
  document.getElementById("moInterval").innerHTML = info;       
}
The final product

When you load the page and move the device around, you should see the values change as the device moves through space and is affected by acceleration.

Try it out, and view the source to see it in action.

Additional resources

Here are a few other resources and demos you can check out that use the HTML5 device orientation or device motion events.

Physics

Acceleration
Acceleration of Gravity
Acceleration of Gravity on Earth
Euler Angles
The Specs

W3C Device Orientation Event Specification
Mozilla DOM Orientation Event
Mozilla Processing Orientation Events
Neat Demos

Pong An experiment to try out device orientation in gaming.
