<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Félix-Antoine Coutu</title>
<style>
   body {
       font-family: Arial, sans-serif;
       text-align: center;
       padding: 10px;
   }

   h1 {
      font-size: 16px !important;
      font-weight: bold;
      color: #333;
      margin: 0;
      border: none;
   }

   .titre-1 {
       margin-bottom: 16px;
   }

   .video-container {
      position: relative;
      display: inline-block;
      width: 100%;
      max-width: 2000px;
      aspect-ratio: 16 / 9;
   }

   iframe {
      width: 100%;
      height: 100%;
   }

   .btn-video {
      position: absolute;
      top: 10px;
      left: 10px;
      width: 150px;
      height: 30px;
      display: flex;
      align-items: center;
      justify-content: center;
      background-color: #433d69;
      color: white;
      font-size: 12px;
      font-weight: bold;
      border: none;
      cursor: pointer;
      border-radius: 3px;
      opacity: 0.8;
      transition: opacity 0.2s, background-color 0.3s;
      z-index: 10;
   }

   .btn-video:hover {
       opacity: 1;
   }

   .btn-salle1 {
       background-color: #194f18;
   }

   .btn-salle2 {
       background-color: #433d69;
   }
</style>
</head>
<body>

<h1 class="titre-1">Fumée Omnisciente, Mirage Onirique | Résidence de création, janvier 2025, Bain Mathieu</h1>

<div class="video-container">
   <iframe id="video" 
      src="https://www.youtube.com/embed/fm00cFcoJM8?enablejsapi=1&modestbranding=1&rel=0&controls=0&disablekb=1" 
      frameborder="0" 
      allowfullscreen>
   </iframe>

   <button id="btnBascule" class="btn-video">Audio salle de droite</button>
</div>

<audio id="audioSalle1" loop>
   <source src="https://www.dropbox.com/scl/fi/ur8dl9pxqmyqqcgq63a2l/FOMO_Audio_Perfo-res-Bain-Mathieu_DRUM.mp3?rlkey=oendf779ij0ijz57i5z65vb8h&st=wya35hdc&raw=1" type="audio/mp3">
</audio>

<audio id="audioSalle2" loop>
   <source src="https://www.dropbox.com/scl/fi/vxsx4wc0ojrao15vsi3rd/FOMO_Audio_Perfo-res-Bain-Mathieu_INSTALL.mp3?rlkey=yuieg0gk2a5t0b6kquxjgoav4&st=15anchfs&raw=1" type="audio/mp3">
</audio>

<script>
    var audioSalle1 = document.getElementById("audioSalle1");
    var audioSalle2 = document.getElementById("audioSalle2");
    var btnBascule = document.getElementById("btnBascule");

    var audioActif = audioSalle2;
    btnBascule.classList.add("btn-salle2");

    var player;
    function onYouTubeIframeAPIReady() {
        player = new YT.Player('video', {
            events: {
                'onStateChange': onPlayerStateChange
            }
        });
    }

    function onPlayerStateChange(event) {
        if (event.data == YT.PlayerState.PLAYING) {
            startSync();
        } else if (event.data == YT.PlayerState.PAUSED) {
            stopSync();
        }
    }

    var syncInterval;
    function startSync() {
        if (!syncInterval) {
            syncAudio();
            syncInterval = setInterval(syncAudio, 500);
        }
    }

    function stopSync() {
        clearInterval(syncInterval);
        syncInterval = null;
        audioActif.pause();
    }

    function syncAudio() {
        if (player && audioActif) {
            var videoTime = player.getCurrentTime();
            var audioDiff = Math.abs(videoTime - audioActif.currentTime);

            if (audioDiff > 0.3) {
                audioActif.currentTime = videoTime;
            }

            if (player.getPlayerState() === YT.PlayerState.PLAYING && audioActif.paused) {
                audioActif.play();
            }
        }
    }

    btnBascule.addEventListener("click", function () {
        if (audioActif === audioSalle1) {
            audioSalle1.muted = true;
            audioSalle2.muted = false;
            audioActif = audioSalle2;
            btnBascule.textContent = "Audio salle de droite";
            btnBascule.classList.remove("btn-salle1");
            btnBascule.classList.add("btn-salle2");
        } else {
            audioSalle1.muted = false;
            audioSalle2.muted = true;
            audioActif = audioSalle1;
            btnBascule.textContent = "Audio salle de gauche";
            btnBascule.classList.remove("btn-salle2");
            btnBascule.classList.add("btn-salle1");
        }

        if (player.getPlayerState() == YT.PlayerState.PLAYING) {
            syncAudio();
        }
    });

    var tag = document.createElement('script');
    tag.src = "https://www.youtube.com/iframe_api";
    var firstScriptTag = document.getElementsByTagName('script')[0];
    firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);
</script>

</body>
</html>
