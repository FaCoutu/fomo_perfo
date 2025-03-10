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
    }
    video {
       width: 100%;
       max-width: 2000px;
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
    <video id="video" controls autoplay>
    <video id="video" controls>
       <source src="https://dl.dropboxusercontent.com/scl/fi/vn856dku4ckgm35azhbz1/Fumee-Omnisciente-Mirage-Onirique02.mp4?rlkey=khuru1f6c5woeclemz1ai9rlz&st=pksoqe29&raw=1" type="video/mp4">    
       Votre navigateur ne prend pas en charge la vidéo HTML5.
    </video>
    <button id="btnBascule" class="btn-video">Audio salle de droite</button>
 </div>
 
 <audio id="audioSalle1" loop>
    <source src="https://www.dropbox.com/scl/fi/5y2aka0keombw6ha0ltg4/FOMO_Audio_Perfo-res-Bain-Mathieu.wav?rlkey=bjy3ssu3mofyg2m5jgvbvwmgl&st=9brcjj0g&raw=1" type="audio/wav">
 </audio>
 
 <audio id="audioSalle2" loop>
    <source src="audio_salle2.mp3" type="audio/mp3">
 </audio>
 
 <script>
     var video = document.getElementById("video");
     var audioSalle1 = document.getElementById("audioSalle1");
     var audioSalle2 = document.getElementById("audioSalle2");
     var btnBascule = document.getElementById("btnBascule");
 
     var audioActif = audioSalle2;
     btnBascule.classList.add("btn-salle2");
 
     video.addEventListener("play", function() {
         if (audioActif.paused) {
             audioActif.currentTime = video.currentTime;
             audioActif.play();
         }
     });
 
     video.addEventListener("pause", function() {
         audioActif.pause();
     });
 
     video.addEventListener("timeupdate", function() {
         if (!video.paused) {
             audioActif.currentTime = video.currentTime;
         }
     });
 
     video.addEventListener("seeked", function() {
         audioActif.currentTime = video.currentTime;
     });
 
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
 
         audioActif.currentTime = video.currentTime;
         if (!video.paused) {
             audioActif.play();
         }
     });
 
     // Fonction pour forcer le bouton en mode plein écran
     function adjustButtonInFullscreen() {
         btnBascule.style.zIndex = "9999"; // Force z-index élevé en mode plein écran
     }
 
     // Fonction pour réinitialiser le bouton lorsque l'on quitte le plein écran
     function resetButtonAfterFullscreen() {
         btnBascule.style.zIndex = "10"; // Réinitialise le z-index lorsque l'on quitte le plein écran
     }
 
     // Rendre le bouton visible et ajuster le z-index en mode plein écran
     document.addEventListener("fullscreenchange", function() {
         if (document.fullscreenElement) {
             adjustButtonInFullscreen();  // Le bouton devient visible avec z-index élevé
         } else {
             resetButtonAfterFullscreen();  // Réinitialisation du z-index
         }
     });
 
     document.addEventListener("webkitfullscreenchange", function() {
         if (document.webkitFullscreenElement) {
             adjustButtonInFullscreen();  // Le bouton devient visible avec z-index élevé
         } else {
             resetButtonAfterFullscreen();  // Réinitialisation du z-index
         }
     });

     // L'utilisateur peut activer le plein écran manuellement en cliquant sur la vidéo
     video.addEventListener("click", function() {
         if (video.requestFullscreen) {
             video.requestFullscreen();
         } else if (video.webkitRequestFullscreen) { // Safari
             video.webkitRequestFullscreen();
         }
     };
     });
 
 </script>
 </body>
 </html>
