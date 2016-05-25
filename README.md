# <img height="80px" src="http://videostream360.com/wp-content/uploads/2015/03/687_VID_Logo_4c_300dpi_200.png" alt="videostream360 Player Logo" title="videostream360 Player Logo"/>

> WE LOVE 360°-LIVE.
> 
> Videostream360 player is the popular 360° video playback for LIVE and OnDemand streams across browsers and file types.
> It empowers you to embed your 360° content in your platform to share your experience with high availability.
> With our interactive backend you can manage multiple streams and append interactive content like hotspots.
> The Javascript API gives your the posibility to programmatically interact with your VR content to create awesome user experiences.
> For more information visit out website: www.videostream360.com
> In our shop you also order a All In One solution with camera included to start right now!


## Content
<!-- MarkdownTOC autolink=true bracket=round depth=2-->

- [Requirements](#requirements)
- [Usage](#usage)
- [Getting started](#getting-started)
- [Options](#options)
- [Funktionen](#funktionen)
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
The interface between backend where you manage your streams and the frontend player is the so called medialist. Thats a JSON file(created by the backend) which is loaded by the player and man 

#### load the player API (Step 1)
Simply put the Cloud Player URL to the <head> of your HTML Page to get the entire access to the API of the player and override default settings.

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
- `medialist` URL path to your medialist. This is the  Pfad zur Projekt-medialist JSON (Diese erhalten sie im Backend)

###optional###
- `playlistbar` Wenn sie mehrere Streams in einem Player anzeigen möchten, können sie die Thumbnail Navigation aktivieren. Über einen Sideclip Button kann er geöffnet und geschlossen werden. Folgende Parameter können verwendet werden:
    + `'show'`: (default) Playlistbar wird angezeigt. (auf Mobile Devices wird er initial automatisch geschlossen)
    +  `'hide'`: Playlistbar ist geschlossen, kann aber über den Sideclip aktiviert werden
    +  `'none'`: kein Playlistbar

*Beispiel:*
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
 
- `controls`: (default: ["media", "compass"] Hier können die Playerelemente Mediacontrol und 360° Kompass ein/ausblenden

*Beispiel:*
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

- `mobileFallback`: Callback Funktion die aufgerufen wird, wenn der HTML5 oder Flash-Player auf dem Gerät nativ nicht unterstützt wird. Sie können somit eine alternative Navigation erstellen, um Streams per URL Scheme in der mobilen App zu öffnen.

## Funktionen

- `ready` : Callback Funktion die aufgerufen wird, sobald der Player initialisiert wurde.

*Beispiel:*
````javascript
    vstream360('vstream360-player').ready(function(){
        alert("ready");
    });
````


- `play` : Methode zum Abspielen des Videos
*Beispiel:*
````javascript
    vstream360('vstream360-player').play();
````

- `pause` : Methode zum Anhalten des Videos
*Beispiel:*
````javascript
    vstream360('vstream360-player').pause();
````

- `stop` : Methode zum Stoppen des Videos
*Beispiel:*
````javascript
    vstream360('vstream360-player').stop();
````

- `dispose` : Löschen der Playerinstanz
*Beispiel:*
````javascript
    vstream360('vstream360-player').dispose();
````


- `seek` : Springen zu einer bestimmten Stelle im Video (nur für onDemand Videos)
*Beispiel:*
````javascript
    vstream360('vstream360-player').seek(5);
````

- `volume` : Einstellen der Lautstärke des Videos von 0 - 1
*Beispiel:*
````javascript
    vstream360('vstream360-player').volume(0.5);
````

- `mute` : Stummschalten der Lautstärke
*Beispiel:*
````javascript
    vstream360('vstream360-player').mute(true);
````


- `enableHotspotMode` : (default: false) Mit diese Methode kann der Hotspotmodus ein und ausgeschalten werden. Somit lassen sich Hotspots per Drag and Drop verschieben.

*Beispiel*
````javascript
vstream360('vstream360-player').enableHotspotMode(true);
````
    
- `onHotspotChanged` : Callback Funktion die aufgerufen wird, wenn ein Hotspot verschoben wurde. Die Funktion liefert die Parameter:
    +  `vangle` - vertikaler Winkel in Grad -90° < 0 < 90°
    +  `hangle` - horizontaler Winkel in Grad: 0 - 360°
    +  `id` - id des Hotspots

*Beispiel*
````javascript
vstream360('vstream360-player').onHotspotChanged(function(data){
    console.log(data);
});
````

- `onHotspotClicked` : Callback Funktion die aufgerufen wird, wenn ein Hotspot geklickt wurde. Die Funktion liefert den Parameter:
    +  `id` - id des Hotspots

*Beispiel*
````javascript
vstream360('vstream360-player').onHotspotClicked(function(data){
    console.log(data.id);
});
````

- `onTimeupdate` : Callback Funktion welche die Abspielposition ausgibt. Die Funktion liefert den Parameter:
    +  `currentTime` - Millisekunden der Abspielposition

*Beispiel*
````javascript
vstream360('vstream360-player').onTimeupdate(function(data){
    console.log(data.currentTime);
});
````


## Demos

http://videostream360.com
