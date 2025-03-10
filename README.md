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
   video {
       width: 100%;
       max-width: 2000px;
       video-align: center;
   }
   button {
       margin: 0px;
       padding: 10px;
       font-size: 12px;
   }
   /* Changer la taille de la police pour les titres */
   h1 {
      font-size: 16px !important;  /* Ajuste la taille ici comme tu le souhaites */
      font-weight: bold;
      color: #5B5B5B; /* Facultatif : change la couleur si nécessaire */
      /* color: #1c5b1b; */
      margin: 0;  /* Empêche les marges par défaut entre les h1 */
      border: none;  /* Enlève les bordures */
   }
   /* Si tu veux ajouter des espacements spécifiques entre les deux titres */
   .titre-1 {
      margin-bottom: 0px;  /* Ajoute un espace après le premier titre */
      margin-top: 0px;  /* Ajoute un espace après le premier titre */  
   }
   .btn-salle1 {
      background-color: #194f18;
      color: white;
   }
   .btn-salle2 {
      background-color: #433d69;
      color: white;
   }
</style>
</head>
<body>

<!-- Premier titre avec une classe pour un espacement -->
<h1 class="titre-1">Fumée Omnisciente, Mirage Onirique | Résidence de création, janvier 2025, Bain Mathieu</h1>

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
   var btnBascule = document.getElementById("btnBascule");
   
   var audioActif = audioSalle2; // On commence avec l'audio de la Salle 2
   btnBascule.textContent = "Audio salle 2"; // Texte initial
   btnBascule.classList.add("btn-salle2"); // Couleur initiale (rouge)
   
   // Démarrage de la vidéo : on synchronise et joue l'audio actif
   video.addEventListener("play", function() {
       if (audioActif.paused) {
           audioActif.currentTime = video.currentTime; // Synchroniser avec la vidéo
           audioActif.play(); // Jouer uniquement l'audio actif
       }
   });
   
   // Mise en pause : on met aussi l'audio actif en pause
   video.addEventListener("pause", function() {
       audioActif.pause();
   });
   
   // Synchroniser la position de l'audio avec la vidéo
   video.addEventListener("timeupdate", function() {
       if (!video.paused) {
           audioActif.currentTime = video.currentTime;
       }
   });
   
   // Lorsqu'on cherche un moment précis dans la vidéo
   video.addEventListener("seeked", function() {
       audioActif.currentTime = video.currentTime;
   });
   
   // Bouton pour basculer entre les pistes audio
   btnBascule.addEventListener("click", function() {
       if (audioActif === audioSalle1) {
           audioSalle1.muted = true;
           audioSalle2.muted = false;
           audioActif = audioSalle2;
           btnBascule.textContent = "Audio salle 2"; // Met à jour le texte du bouton
   
           // Mise à jour des couleurs
           btnBascule.classList.remove("btn-salle1");
           btnBascule.classList.add("btn-salle2");
   
       } else {
           audioSalle1.muted = false;
           audioSalle2.muted = true;
           audioActif = audioSalle1;
           btnBascule.textContent = "Audio salle 1"; // Met à jour le texte du bouton
   
           // Mise à jour des couleurs
           btnBascule.classList.remove("btn-salle2");
           btnBascule.classList.add("btn-salle1");
       }
   
       // Synchroniser et jouer immédiatement l'audio actif
       audioActif.currentTime = video.currentTime;
       if (!video.paused) {
           audioActif.play();
       }
   });
</script>

</body>
</html>
