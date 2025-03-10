<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Félix-Antoine Coutu</title>
<style>
   body {
       font-family: Arial, sans-serif;
       text-align: center;
       padding: 16px;
   }
   video {
       width: 100%;
       max-width: 2000px;
   }
   button {
       margin: 30px;
       padding: 20px;
       font-size: 12px;
   }
   /* Changer la taille de la police pour les titres */
   h1 {
      font-size: 16px !important;  /* Ajuste la taille ici comme tu le souhaites */
      font-weight: bold;
      color: #333;  /* Facultatif : change la couleur si nécessaire */
      margin: 0;  /* Empêche les marges par défaut entre les h1 */
      border: none;  /* Enlève les bordures */
   }
   /* Si tu veux ajouter des espacements spécifiques entre les deux titres */
   .titre-1 {
      margin-bottom: 0px;  /* Ajoute un espace après le premier titre */
   }
</style>
</head>
<body>

<!-- Premier titre avec une classe pour un espacement -->
<h1 class="titre-1">Fumée Omnisciente, Mirage Onirique</h1>

<!-- Deuxième titre, sans classe spécifique, donc prendra les mêmes styles -->
<h1>Résidence de création, janvier 2025, Bain Mathieu</h1>

<!-- Vidéo divisée en deux (les deux salles) -->
<video id="video" controls autoplay>
   <source src="https://dl.dropboxusercontent.com/scl/fi/vn856dku4ckgm35azhbz1/Fumee-Omnisciente-Mirage-Onirique02.mp4?rlkey=khuru1f6c5woeclemz1ai9rlz&st=pksoqe29&raw=1" type="video/mp4">    
   Votre navigateur ne prend pas en charge la vidéo HTML5.
</video>

<!-- Pistes audio -->
<audio id="audioSalle1" loop>
   <source src="https://www.dropbox.com/scl/fi/5y2aka0keombw6ha0ltg4/FOMO_Audio_Perfo-res-Bain-Mathieu.wav?rlkey=bjy3ssu3mofyg2m5jgvbvwmgl&st=9brcjj0g&raw=1" type="audio/wav">
   Votre navigateur ne prend pas en charge l'audio.
</audio>
<audio id="audioSalle2" loop>
   <source src="audio_salle2.mp3" type="audio/mp3">
   Votre navigateur ne prend pas en charge l'audio.
</audio>

<!-- Boutons de contrôle -->
<button id="btnBascule">Appuyer ici pour basculer entre l'audio de la première et de la seconde salle</button>

  <!-- Script JavaScript intégré -->
  <script>
     var audioSalle1 = document.getElementById("audioSalle1");
     var audioSalle2 = document.getElementById("audioSalle2");
     var video = document.getElementById("video");
  
     var audioActif = null;  // Variable pour mémoriser l'audio actif
  
     // Lors du démarrage de la vidéo
     video.addEventListener("play", function() {
         audioSalle1.play();
         audioSalle2.play();
         audioSalle1.muted = true;  // D'abord, on mute l'audio de la salle 1
         audioActif = audioSalle2;  // Mémoriser l'audio actif (Salle 2)
     });
  
     // Lors de la mise en pause de la vidéo
     video.addEventListener("pause", function() {
         // Mémoriser l'audio actif au moment de la pause
         if (!audioSalle1.muted) {
             audioActif = audioSalle1;
         } else {
             audioActif = audioSalle2;
         }
  
         // Mettre les deux audios en pause
         audioSalle1.pause();
         audioSalle2.pause();
     });
  
     // Lors de la reprise de la vidéo après une pause
     video.addEventListener("play", function() {
         if (audioActif) {
             audioActif.play();  // Reprendre l'audio actif
             audioActif.currentTime = video.currentTime;  // Synchroniser l'audio avec la vidéo
         }
     });
  </script>
</body>
</html>
