<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Félix-Antoine Coutu</title>
<style>
   body {
       font-family: Arial, sans-serif;
       text-align: center;
       background-color: grey;
       padding: 10px;
   }

   h1 {
      font-size: 16px !important;
      font-weight: bold;
      color: #333;
      margin: 0;
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
</style>
</head>
<body>

<h1 class="titre-1">Fumée Omnisciente, Mirage Onirique | Résidence de création, janvier 2025, Bain Mathieu</h1>

<div class="video-container">
   <iframe id="video" 
      src="https://www.youtube.com/embed/fm00cFcoJM8?enablejsapi=1&modestbranding=1&rel=0&iv_load_policy=3&controls=0" 
      frameborder="0" allow="autoplay" allowfullscreen>
   </iframe>
   <button id="btnBascule" class="btn-video">Audio salle de droite</button>
</div>

<audio id="audioSalle1" loop>
   <source src="https://www.dropbox.com/scl/fi/ur8dl9pxqmyqqcgq63a2l/FOMO_Audio_Perfo-res-Bain-Mathieu_DRUM.mp3?raw=1" type="audio/mp3">
</audio>

<audio id="audioSalle2" loop>
   <source src="https://www.dropbox.com/scl/fi/vxsx4wc0ojrao15vsi3rd/FOMO_Audio_Perfo-res-Bain-Mathieu_INSTALL.mp3?raw=1" type="audio/mp3">
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
            events: { 'onStateChange': onPlayerStateChange }
        });
    }

    function onPlayerStateChange(event) {
        if (event.data == YT.PlayerState.PLAYING) startSync();
        else if (event.data == YT.PlayerState.PAUSED) stopSync();
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
            if (Math.abs(videoTime - audioActif.currentTime) > 0.3) {
                audioActif.currentTime = videoTime;
            }
            if (player.getPlayerState() === YT.PlayerState.PLAYING && audioActif.paused) {
                audioActif.play();
            }
        }
    }

    btnBascule.addEventListener("click", function () {
        audioActif.muted = true;
        audioActif = (audioActif === audioSalle1) ? audioSalle2 : audioSalle1;
        audioActif.muted = false;
        btnBascule.textContent = (audioActif === audioSalle1) ? "Audio salle de gauche" : "Audio salle de droite";
        if (player.getPlayerState() == YT.PlayerState.PLAYING) {
            syncAudio();
        }
    });

    var tag = document.createElement('script');
    tag.src = "https://www.youtube.com/iframe_api";
    document.getElementsByTagName('script')[0].parentNode.insertBefore(tag, null);
</script>

</body>
</html>
