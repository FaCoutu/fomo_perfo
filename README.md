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
         .video-container {
             position: relative;
             display: inline-block;
             width: 100%;
             max-width: 2000px; /* Optionnel, pour limiter la largeur maximum */
             height: 0;
             padding-bottom: 56.25%; /* 16:9 Aspect Ratio */
         }
         .video-container iframe {
             position: absolute;
             top: 0;
             left: 0;
             width: 100%;
             height: 100%;
         }
         .btn-video {
             position: absolute;
             top: 10px;
             left: 10%;
             transform: translateX(-50%);
             background-color: #433d69;
             color: white;
             padding: 10px 20px;
             border: none;
             font-size: 14px;
             cursor: pointer;
             border-radius: 5px;
             opacity: 0.8;
             transition: opacity 0.3s, background-color 0.3s;
             z-index: 10;
             text-align: left;
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
     <iframe id="video" src="https://www.youtube.com/embed/fm00cFcoJM8?enablejsapi=1" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
     <button id="btnBascule" class="btn-video">Audio salle de droite</button>
 </div>
 
 <audio id="audioSalle1" loop>
     <source src="https://www.dropbox.com/scl/fi/xslc65agq0msywqp9w1px/FOMO_Audio_Perfo-res-Bain-Mathieu.mp3?rlkey=uecntb0ntbjg7dau3m46smpy8&st=lhe0s2ao&raw=1" type="audio/wav">
 </audio>
 
 <audio id="audioSalle2" loop>
     <source src="audio_salle2.mp3" type="audio/mp3">
 </audio>
 
 <script>
     var audioSalle1 = document.getElementById("audioSalle1");
     var audioSalle2 = document.getElementById("audioSalle2");
     var btnBascule = document.getElementById("btnBascule");
     
     var audioActif = audioSalle2;
     btnBascule.classList.add("btn-salle2");
     
     var player;
     var lastSyncTime = 0;  // Variable pour suivre la dernière synchronisation
     var isAudioPlaying = false; // Ajout d'une variable pour suivre l'état de l'audio
     
     // Fonction d'initialisation de l'API YouTube
     function onYouTubePlayerAPIReady() {
         player = new YT.Player('video', {
             events: {
                 'onStateChange': onPlayerStateChange,
             }
         });
     }
     
     // Quand l'état de la vidéo change (lecture, pause, etc.)
     function onPlayerStateChange(event) {
         if (event.data == YT.PlayerState.PLAYING) {
             if (!isAudioPlaying) {
                 audioActif.currentTime = player.getCurrentTime();
                 audioActif.play();
                 isAudioPlaying = true;  // Assurer que l'audio commence à jouer uniquement une fois
             }
         } else if (event.data == YT.PlayerState.PAUSED) {
             audioActif.pause();
             isAudioPlaying = false;  // Mettre à jour l'état pour indiquer que l'audio est en pause
         }
     }
     
     // Synchronisation de l'audio et de la vidéo en fonction du temps
     setInterval(function() {
         if (player && player.getPlayerState() !== YT.PlayerState.PAUSED) {
             var currentTime = player.getCurrentTime();
     
             // Synchroniser l'audio toutes les 100ms si le temps a changé de plus de 0.1s
             if (Math.abs(currentTime - lastSyncTime) > 0.1) {
                 audioActif.currentTime = currentTime;
                 lastSyncTime = currentTime;  // Mettre à jour la dernière synchronisation
             }
         }
     }, 100);
     
     // Changer l'audio actif à la demande
     btnBascule.addEventListener("click", function() {
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
     
         // Synchroniser l'audio avec la vidéo mais éviter de le redémarrer trop souvent
         if (isAudioPlaying) {
             audioActif.currentTime = player.getCurrentTime();
         } else {
             // Assurer que l'audio démarre au bon moment
             audioActif.currentTime = player.getCurrentTime();
             audioActif.play();
             isAudioPlaying = true;
         }
     });
     
     // Charger l'API YouTube Iframe Player
     var tag = document.createElement('script');
     tag.src = "https://www.youtube.com/iframe_api";
     var firstScriptTag = document.getElementsByTagName('script')[0];
     firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);
 </script>
 
 </body>
 </html>
