The current version is meant for watching on a firestick. Specifically, the Amazon Silk web browser on the firestick. 
Additioanlly, change the URL at the bottom of the code to change the streams being displayed. 

The firestick version supports three streams while the PC version only supports two streams

Here is the code for a PC version which can be hosted on your local computer:

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Football Split-Screen Streaming</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background-color: #1a1a1a;
            color: rgb(0, 132, 255);
            display: flex;
            flex-direction: column;
            min-height: 100vh;
            overflow: hidden;
        }

        .title-container {
            display: flex;
            justify-content: space-between;
            width: 100%;
            padding: 10px 20px;
        }

        .container {
            display: flex;
            width: 100%;
            height: 100%;
            margin-top: 225px;
        }

        .video-frame {
            flex: 1;
            height: 100%;
            background-color: #1a1a1a;
            overflow: hidden;
        }

        .video-frame video {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .separator {
            position: absolute;
            top: 0;
            left: 50%;
            width: 6px;
            height: 1000vh;
            background-color: rgb(0, 132, 255);
            transform: translateX(-50%);
            z-index: 0;
        }

    </style>
</head>
<body>

    <div class="container">
        <div class="video-frame">
            <video id="video1" controls></video>
        </div>
        <div class="separator"></div>
        <div class="video-frame">
            <video id="video2" controls></video>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/hls.js@latest"></script>
    <script>
        function initializeVideo(videoId, streamUrl) {
            const video = document.getElementById(videoId);
            if (Hls.isSupported()) {
                const hls = new Hls({
                    maxBufferLength: 60,
                    maxMaxBufferLength: 120
                });
                hls.loadSource(streamUrl);
                hls.attachMedia(video);
                hls.on(Hls.Events.MANIFEST_PARSED, () => video.play());
            } else if (video.canPlayType('application/vnd.apple.mpegurl')) {
                video.src = streamUrl;
                video.addEventListener('loadedmetadata', () => video.play());
            }
        }

        initializeVideo('video1', 'https://main.clmbosean.space/playlist/26584/main.clmbosean.space/caxi.m3u8'); //CHANGE FOR DIFFERENT STREAM 
        initializeVideo('video2', 'https://main.clmbosean.space/playlist/25608/main.clmbosean.space/caxi.m3u8'); //CHANGE FOR DIFFERENT STREAM 


        //MIGHT NEED TO RUN THIS: 
        //1. cd "C:/Users/jonat/OneDrive/Desktop/Code/HtmlRandom/"
        //2. python -m http.server 8000

        
    </script>
</body>
</html>
