<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lecteur Minimaliste</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #111;
            color: white;
        }

        #video-container {
            position: relative;
            width: 80%;
            max-width: 800px;
            margin: auto;
        }

        #player {
            width: 100%;
            height: 450px;
            background: black;
        }

        #playButton {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: rgba(255, 255, 255, 0.8);
            border: none;
            border-radius: 50%;
            width: 60px;
            height: 60px;
            font-size: 24px;
            font-weight: bold;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        #playButton.hidden {
            display: none;
        }
    </style>
</head>
<body>

    <h1>Lecteur Minimaliste YouTube</h1>

    <div id="video-container">
        <div id="player"></div>
        <button id="playButton">▶️</button>
    </div>

    <script>
        var player;
        function onYouTubeIframeAPIReady() {
            player = new YT.Player('player', {
                videoId: 'fm00cFcoJM8',
                playerVars: {
                    'modestbranding': 1,
                    'rel': 0,
                    'controls': 0,
                    'disablekb': 1
                },
                events: {
                    'onReady': onPlayerReady
                }
            });
        }

        function onPlayerReady(event) {
            var playButton = document.getElementById("playButton");
            playButton.addEventListener("click", function () {
                if (player.getPlayerState() === 1) {
                    player.pauseVideo();
                    playButton.textContent = "▶️";
                } else {
                    player.playVideo();
                    playButton.textContent = "⏸️";
                    playButton.classList.add("hidden"); // Cache le bouton après lecture
                }
            });
        }

        // Chargement de l'API YouTube
        var tag = document.createElement('script');
        tag.src = "https://www.youtube.com/iframe_api";
        var firstScriptTag = document.getElementsByTagName('script')[0];
        firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);
    </script>

</body>
</html>
