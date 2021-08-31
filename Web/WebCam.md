
# WebCam

### navigator.MediaDevices.getUserMedia()
```bash
# FYI:  Support was initially provided by the Navigator.getUserMedia() method, but this has been deprecated.
# You should now use the navigator.MediaDevices.getUserMedia() method

https://www.w3schools.com/js/js_window_navigator.asp
navigator.mediaDevices.getUserMedia()   Use this
          MediaDevices.getUserMedia()   has been deprecated
https://developer.mozilla.org/en-US/docs/Web/API/Navigator/getUserMedia
```

---

### Capturing Audio & Video in HTML5
https://www.html5rocks.com/en/tutorials/getusermedia/intro/

### Demo: simpl.info MediaStreamTrack.getSources
https://simpl.info/getusermedia/sources/

### Real time communication with WebRTC
https://codelabs.developers.google.com/codelabs/webrtc-web/#0

### WebRTC in the real world: STUN, TURN and signaling
https://www.html5rocks.com/en/tutorials/webrtc/infrastructure/  
https://github.com/niklasenbom/RecordingApp


### Choose Cameras, Microphones and Speakers from Your Web App
https://developers.google.com/web/updates/2015/10/media-devices

### Chrome 47 WebRTC: Media Recording, Secure Origins and Proxy Handling
https://developers.google.com/web/updates/2015/10/chrome-47-webrtc?hl=en


### Accessing Your Webcam in HTML
https://www.kirupa.com/html5/accessing_your_webcam_in_html5.htm

Camera and Video Control with HTML5
https://davidwalsh.name/browser-camera


### Camvas
https://github.com/cbrandolino/camvas


### Getting Started with Web Audio API
https://www.html5rocks.com/en/tutorials/webaudio/intro/  
- [Getting Started with WebRTC](https://www.html5rocks.com/en/tutorials/webrtc/basics/#toc-mediastream)
- [Google I/O 2012 - WebRTC: Real-time Audio/Video and P2P in HTML5](https://www.youtube.com/watch?v=E8C8ouiXHHk)
- [WebRTC Tutorial - How does WebRTC work?](WebRTC Tutorial - How does WebRTC work?)


### Live Stream Using HTML 5 and Node.js
https://github.com/tiagobutzke/LiveWebcamWithHTML5

### Stream a webcam using Javascript, NodeJS, Android, Opera Mobile, Web Sockets and HTML5
http://francisshanahan.com/index.php/2011/stream-a-webcam-using-javascript-nodejs-android-opera-mobile-web-sockets-and-html5/

### Unreal Webcam Fun with getUserMedia() and HTML5 Canvas
https://www.youtube.com/watch?v=ElWFcBlVk-o

## serverless-webrtc
- [serverless-webrtc](https://blog.printf.net/articles/2013/05/17/webrtc-without-a-signaling-server/)
- [Github: serverless-webrtc](https://github.com/cjb/serverless-webrtc)


## WebSockets

### Introducing WebSockets: Bringing Sockets to the Web
https://www.html5rocks.com/en/tutorials/websockets/basics/

### How JavaScript works: Deep dive into WebSockets and HTTP/2 with SSE + how to pick the right path
https://blog.sessionstack.com/how-javascript-works-deep-dive-into-websockets-and-http-2-with-sse-how-to-pick-the-right-path-584e6b8e3bf7

### WebSockets, HTTP/2, and SSE
https://medium.com/axiomzenteam/websockets-http-2-and-sse-5c24ae4d9d96

### Do you really need WebSockets
https://blog.stanko.io/do-you-really-need-websockets-343aed40aa9b

### RTCPeerConnection without servers


---
# Server Sent Events (SSE)
The idea of Server Sent Events is to provide a standard way for you to open a connection and push data unilaterally from the server to the client. Let’s check an example

```JavaScript
// Server implementation of SSE

const http = require('http');

const server = http.createServer(function (req, res) {
  if (req.url === '/live') {
    res.writeHead(200, {
      'Content-Type': 'text/event-stream',
      'Cache-Control': 'no-cache',
      'Connection': 'keep-alive'
    });
    res.write('retry: 5000\n');

    const interval = setInterval(() => {
      res.write('data: ' + new Date() + '\n\n');
    }, 1000);

    req.on('end', () => clearInterval(interval));
    return;
  }

  // Normal requests
  return res.end();
});

server.listen(3000);
```

#### Client implementation of SSE
```html
<script>
  var source = new EventSource('/live');
  source.onmessage = function(event) {
    console.log('Incoming date:' + event.data);
  };
</script>
```