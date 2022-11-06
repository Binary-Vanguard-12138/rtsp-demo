# rtsp-demo
Sample RTSP demo project with server and client

# Reference Link
* [Install FFMpeg on CentOS7](https://linuxize.com/post/how-to-install-ffmpeg-on-centos-7/)
* https://stackoverflow.com/questions/23011302/best-approach-to-get-rtsp-streaming-into-web-browser-from-ip-camera

## server
ffmpeg -i rtsp://sabat:asdf259090@110.39.5.211:554/Streaming/Channels/101 -f mpegts -codec:v mpeg1video -s 320x240 -b 800k -r 30 http://localhost:8082/password
node websocket-relay.js password 8082 27017

