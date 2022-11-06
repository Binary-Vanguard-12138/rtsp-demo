# rtsp-demo

Sample RTSP demo project with server and client

# Reference Link

-   [Best approach to get RTSP streaming into web browser from IP Camera?](https://stackoverflow.com/questions/23011302/best-approach-to-get-rtsp-streaming-into-web-browser-from-ip-camera)
-   [HTML5 Live Video Streaming via WebSockets](https://phoboslab.org/log/2013/09/html5-live-video-streaming-via-websockets)
-   [JSMpeg – MPEG1 Video & MP2 Audio Decoder in JavaScript](https://github.com/phoboslab/jsmpeg.git)

# Running Demo

## Server

### Prerequisites

#### Install FFMPEG

You can refer to the following link to install FFMPEG libaray on CentOS7.

[Install FFMpeg on CentOS7](https://linuxize.com/post/how-to-install-ffmpeg-on-centos-7/)

#### Install npm packages

Change into server directory and run `npm install ws` to install npm dependency packages.

```
cd server
npm install ws
```

### Run server

First you will need to run HTTP-Websocket relay server.

```
node websocket-relay.js supersecretpassword 8081 27017
```

Here you should provide the password for authentication, HTTP listening port and Websocket listening port.

Next you will need to run ffmpeg program to receive RTSP stream from the server and push it to the relay server as HTTP traffic.

```
ffmpeg -i rtsp://<any rtsp stream URL> -f mpegts -codec:v mpeg1video -s 320x240 -b 800k -r 30 http://localhost:8081/supersecretpassword
```

Here the output format MUST be `mpegts`, since jsmpeg library which is used on the client side only supports this format. Video size parameter can be given by `-s 320x240`.

## Client

In the `client` directory, we have 1 html and 1 js file.
In the `view-stream.html` file, you can find the websocket URL and you should replace it with the address of your own relay server.

```
var canvas = document.getElementById('video-canvas');
// var url = 'ws://'+document.location.hostname+':8082/';
var url = 'ws://89.40.7.94:27017/';
var player = new JSMpeg.Player(url, {canvas: canvas});
```

If you open the html file, you can see the shining video streams. 😎
