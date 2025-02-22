## FEEL FREE TO USE IT | The source URL is in HLS format, not DASH.

cloudseventv by Amirah

<p align="center"> 
  Visitor Count<br>
  <img src="https://raw.githubusercontent.com/javascript-obfuscator/javascript-obfuscator/master/images/logo.png" />
</p>

---

## HLS & DASH Stream checker HTML Format
This tool is suitable for use on Android and iOS devices.

It can check at least 8 URLs simultaneously.

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>HLS & DASH Multi Stream Checker</title>
    <script src="https://cdn.jsdelivr.net/npm/hls.js@latest"></script>
    <script src="https://cdn.dashjs.org/latest/dash.all.min.js"></script>
    <style>
        body {
            text-align: center;
            background-color: black;
            color: white;
            font-family: Arial, sans-serif;
        }
        video {
            width: 90%;
            max-width: 600px;
            border: 2px solid white;
            margin-top: 20px;
        }
        .stream-container {
            margin-bottom: 20px;
        }
        #status {
            font-size: 20px;
            font-weight: bold;
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <h2>🔍 HLS & DASH Multi Stream Checker</h2>
    <textarea id="streamUrls" placeholder="Enter HLS (m3u8) or DASH (MPD) URLs, one per line" rows="5" cols="50"></textarea>
    <br>
    <button onclick="checkStreams()">Check Streams</button>
    
    <div id="streams"></div>

    <script>
        function checkStreams() {
            let urls = document.getElementById("streamUrls").value.split("\n").map(url => url.trim()).filter(url => url);
            let container = document.getElementById("streams");
            container.innerHTML = "";
            
            urls.forEach(url => {
                let div = document.createElement("div");
                div.classList.add("stream-container");
                
                let statusText = document.createElement("p");
                statusText.innerText = `Checking: ${url}`;
                statusText.style.color = "yellow";
                
                let video = document.createElement("video");
                video.controls = true;
                video.playsInline = true;
                video.style.display = "none";
                
                div.appendChild(statusText);
                div.appendChild(video);
                container.appendChild(div);
                
                fetch(url)
                    .then(response => {
                        if (response.ok) {
                            statusText.innerText = `✅ Stream is Live: ${url}`;
                            statusText.style.color = "lime";
                            video.style.display = "block";
                            playStream(url, video);
                        } else {
                            statusText.innerText = `❌ Stream is Down: ${url}`;
                            statusText.style.color = "red";
                        }
                    })
                    .catch(() => {
                        statusText.innerText = `❌ Stream is Down: ${url}`;
                        statusText.style.color = "red";
                    });
            });
        }

        function playStream(url, video) {
            if (url.endsWith(".m3u8")) {
                if (Hls.isSupported()) {
                    let hls = new Hls();
                    hls.loadSource(url);
                    hls.attachMedia(video);
                    hls.on(Hls.Events.MANIFEST_PARSED, function () {
                        video.play();
                    });
                } else if (video.canPlayType('application/vnd.apple.mpegurl')) {
                    video.src = url;
                    video.addEventListener('loadedmetadata', function () {
                        video.play();
                    });
                } else {
                    alert("HLS is not supported in this browser.");
                }
            } else if (url.endsWith(".mpd")) {
                if (window.dashjs) {
                    let player = dashjs.MediaPlayer().create();
                    player.initialize(video, url, true);
                } else {
                    alert("DASH is not supported in this browser.");
                }
            } else {
                alert("Invalid stream format. Only HLS (.m3u8) and DASH (.mpd) are supported.");
            }
        }
    </script>
</body>
</html>

