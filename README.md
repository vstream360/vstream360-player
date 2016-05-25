# <img height="80px" src="http://videostream360.com/wp-content/uploads/2015/03/687_VID_Logo_4c_300dpi_200.png" alt="videostream360 Player Logo" title="videostream360 Player Logo"/>

> WE LOVE 360°-LIVE.
> 
>videostream360’s panoramic player is the smart and easy-to-use 360° video playback for LIVE and OnDemand streams on any browser and file type. It is based on HTML5 WebGL. If a device doesn't support this feature the Flashplayer fallback will be called up automatically or - on mobile devices - the Mobile App that works with URL'scheme will take over. 
>
>The player empowers you to embed your 360° content in your platform to share your experience with high availability. With our interactive backend platform you can manage multiple streams and append interactive content like clickable hotspots. The Javascript API gives your the possibility to programmatically interact with your VR content to create awesome user experiences. 


## Content
<!-- MarkdownTOC autolink=true bracket=round depth=2-->

- [Requirements](#requirements)
- [Usage](#usage)
- [Options](#options)
- [Functions](#functions)
- [Demos](#demos)

<!-- /MarkdownTOC -->


## Requirements
To start with the 360° player you have to create a licence first on http://shop.videostream360.com. Create a new event in the interactive backend to get your eventID and use the cloudhosted player. The backend is the central WYSIWYG platform to manage all your 360° degree settings like hotspots, watermark, playlists and much more with. 
That's all!


## Usage
You can use the player as:
- <embed code> iFrame
- WordPress Plugin
- with the Javascript API to interact programmatically with the player
- Mobile App

### embed as iFrame

````html
<iFrame src="//cdn.vstream360.net/<eventID>/index.html"
    width="800"
    height="450"
    frameborder="0"
    frameBorder="0"
    scrolling="no" 
    allowfullscreen
>no iframes fallback</iframe>
````

### Use Javascript API
The interface between backend where you manage your streams and the frontend player is the so called medialist. Thats a JSON file(created by the backend) which is loaded by the player and manage the video settings.

#### load the player API (Step 1)
Simply put the cloud player URL to the <head> of your HTML Page to get the entire access to the API of the player and override default settings.

````html
<script type="text/javascript" src="//cdn.vstream360.net/<eventID>/player/vstream360.js"></script>
````


#### create a player (Step 2)
Once the player is placed in the <head> of your code write the embed code for your page <body> where you'd like your player to appear.

*Minimum example:*
````html
<div id="vstream360-player"></div>

<script>
    vstream360('vstream360-player').create({
        'width' : '100%',
        'height' : '100%',
        'primary' : 'auto',
        'medialist' : '<medialist>'
        }
    });

</script>
````



## Options
vstream360(`<ID of html dom element>`).create({`options`});

###required###
- `width`:  (value in `%` or `px`) Width of the player
- `height`: (value in `%` or `px`) Height of the player
- `primary`: (default `'auto'`) Playback Platform. [Possible values: `'auto'`, `'html5'`, `'flash'`]
- `medialist` URL path to your medialist. (Displayed in the Backend)

###optional###
- `playlistbar` If you've created more than one stream a playlist with thumbnails appears at the right side of the player. Users can open and close this playlist with a button. Use the following parameters to setup this playlistbar:
    + `'show'`: (default) show the playlistbar. (On mobile devices it have the closed status initialiy)
    +  `'hide'`: playlistbar is closed but the toggle button appears to open it.
    +  `'none'`: no playlistbar will be created

*Example:*
````javascript

    vstream360('vstream360-player').create({
        'width' : '100%',
        'height' : '100%',
        'primary' : 'auto',
        'medialist' : '//cdn.vstream360.net/<eventID>/medialist.json',
        'playlistbar' : 'show'
        }
    });

````
 
- `controls`: (Array default: ["media", "compass"] You can define if mediacontrols or 360° compass (at the top of the player) should be visible

*Example:*
````javascript

    vstream360('vstream360-player').create({
        'width' : '100%',
        'height' : '100%',
        'primary' : 'auto',
        'medialist' : '//cdn.vstream360.net/<eventID>/medialist.json',
        'controls' : ["media", "compass"]
        }
    });

````

- `mobileFallback`: If your platform doesn't A callback function which is triggered if the mobile app fallback selected.

## Functions

- `ready` : A callback function that is called when player is created and ready to play. This function returs two parameters.
    + `'mode'`: String: 'html5' or 'flash'
    + `'data'`: JSON Object: the full medialist content. So you can handle data like geolocation to create maps or other interactive stuff.
    
*Example:*
````javascript
    vstream360('vstream360-player').ready(function(mode, data){
        console.log("ready: " + mode);
        console.log("ready: " + data);
    });
````


- `play` : Method to play the current loaded stream
*Example:*
````javascript
    vstream360('vstream360-player').play();
````

- `pause` : Method to pause the current loaded stream
*Example:*
````javascript
    vstream360('vstream360-player').pause();
````

- `stop` : Method to stop the current loaded stream
*Example:*
````javascript
    vstream360('vstream360-player').stop();
````

- `dispose` : Method to stop the current loaded stream and delete the player instance.
*Example:*
````javascript
    vstream360('vstream360-player').dispose();
````


- `seek` : Method to jump to a specific position of the stream(For onDemand). Value in seconds.
*Example:*
````javascript
    vstream360('vstream360-player').seek(5);
````

- `volume` : Set up the volume of the player (values between: 0 - 1)
*Example:*
````javascript
    vstream360('vstream360-player').volume(0.5);
````

- `mute` : Mutes the player
*Example:*
````javascript
    vstream360('vstream360-player').mute(true);
````


- `enableHotspotMode` : (default: false) Method to enable the hotspot drag mode. So you can move hotspots an get the new position.

*Example*
````javascript
vstream360('vstream360-player').enableHotspotMode(true);
````
    
- `onHotspotChanged` : Callback function that is called if the hotspot is moved. This function returns the follwing parameters:
    +  `vangle` - vertical arrow in degrees -90° < 0 < 90°
    +  `hangle` - horizontal arrow in degrees: 0 - 360°
    +  `id` - id of the motspot that is moved

*Example*
````javascript
vstream360('vstream360-player').onHotspotChanged(function(data){
    console.log(data);
});
````

- `onHotspotClicked` : Callback function that is called if a hotspot was clicked. Use this to handle User interactions. This function returns the follwing parameters:
    +  `id` - id of the hotspot

*Example*
````javascript
vstream360('vstream360-player').onHotspotClicked(function(data){
    console.log(data.id);
});
````

- `onTimeupdate` : Callback function to get the playheadtime of the video. It returns the following parmeters:
    +  `currentTime` - milliseconds of the position

*Example*
````javascript
vstream360('vstream360-player').onTimeupdate(function(data){
    console.log(data.currentTime);
});
````


## Demos

## Further infomation
http://www.videostream360.com
http://shop.videostream360.com
