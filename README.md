# videostream360 player
Der erste 360°-Livestream-Player in HTML5 mit Backend zur Verwaltung von Livestreams, interaktiven Hotspots und vielem mehr.
Für weitere Informationen besuchen sie unsere Website: www.videostream360.com

## Inhalt
<!-- MarkdownTOC autolink=true bracket=round depth=2-->

- [Voraussetzung](#voraussetzung)
- [Installation](#installation)
- [Getting started](#getting-started)
- [Optionen](#optionen)
- [Funktionen](#funktionen)
- [Demos](#demos)

<!-- /MarkdownTOC -->



## Voraussetzung
Grundlage für die Benutzung des Players ist ein gültiger Lizenzcode (Licence ID). Entscheiden sie welches Produkt für sie das richtige ist und erstellen sie sich eine neue Lizenz. http://show.videostream360.com

Anschließend können sie sofort beginnen und ihren eigenen 360° Player als iFrame in ihre Seite einbinden. Oder aber verwenden sie die Javascript API, um gezielt die Funktionen des Players zu steuern.


## Installation

### per iFrame

````html
<iFrame src="//cdn.vstream360.net/assets/<licenceID>/index.html"
    width="800"
    height="450"
    frameborder="0"
    frameBorder="0"
    scrolling="no" 
    allowfullscreen
>no iframes fallback</iframe>
````

### per Javascript
Zunächste muss der vstream360.js Player in den HEAD des THML Dokuments eingebunden werden:

````html
<script type="text/javascript" src="//cdn.vstream360.net/<licenceID>/player/vstream360.js"></script>
````



## Getting started

***Initialisierung des Player***

Zuerst wird ein `<div />` erstellt und eine id vergeben. Nun kann der Player initialisiert werden, indem man im die ID des HTML Elements übergibt: vstream360(`id des html elements`).create({`options`});

*Beispiel*
````html
<div id="my-vstream360-player"></div>

<script>
    vstream360('vstream360-player').create({
        'width' : '100%',
        'height' : '100%',
        'primary' : 'auto',
        'medialist' : '//cdn.vstream360.net/assets/<licenceID>/medialist.json'
        }
    });

</script>
````


## Optionen
###required###
- `width`:  (value in `%` or `px`) Breite des Players
- `height`: (value in `%` or `px`) Breite des Players
- `primary`: (default `'auto'`) Playback Platform. Erlaube Strings `'auto'`, `'html5'`, `'flash'`
- `medialist` Pfad zur Projekt-medialist (Diese wird im Backend angezeigt)

###optional###
- `playlistbar` Wenn sie mehrere Streams in einem Player anzeigen möchten, können sie die Thumbnail Navigation aktivieren. Geben sie dazu die Position `position` und die Breite `size` in `px` an.

- `controls`: (default: ["media", "compass"] Hier können die Playerelemente Mediacontrol und 360° Kompass ein/ausblenden

*Beispiel:*
````javascript

    vstream360('vstream360-player').create({
        'width' : '100%',
        'height' : '100%',
        'primary' : 'auto',
        'medialist' : '//cdn.vstream360.net/assets/<licenceID>/medialist.json',
        'playlistbar' : {'position' : 'right', 'size': 180}
        }
    });

````

- `playlistbar' : {position : 'right', size: 180}`
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



## Demos

http://videostream360.com
