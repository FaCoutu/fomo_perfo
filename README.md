<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Félix-Antoine Coutu</title>
<style>
   body {
       font-family: Arial, sans-serif;
       text-align: center;
       padding: 30px;
   }
   video {
       width: 150%;
       max-width: 4000px;
   }
   button {
       margin: 10px;
       padding: 40px;
       font-size: 12px;
   }
   /* Changer la taille de la police pour les titres */
   h1 {
      font-size: 16px !important;  /* Ajuste la taille ici comme tu le souhaites */
      font-weight: bold;
      /*color: #5B5B5B; */ /* Facultatif : change la couleur si nécessaire */
      color: #1c5b1b;
      margin: 0;  /* Empêche les marges par défaut entre les h1 */
      border: none;  /* Enlève les bordures */
   }
   /* Si tu veux ajouter des espacements spécifiques entre les deux titres */
   .titre-1 {
      margin-bottom: 0px;  /* Ajoute un espace après le premier titre */
      margin-top: 0px;  /* Ajoute un espace après le premier titre */
      
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

    // Variable pour mémoriser l'audio actif (avant la pause)
    var audioActif = null;

    // Lors du démarrage de la vidéo
    video.addEventListener("play", function() {
        audioSalle1.play();
        audioSalle2.play();
        audioSalle1.muted = true;  // D'abord, mute l'audio de la salle 1
        audioSalle2.muted = false; // L'audio de la salle 2 est actif
        audioActif = audioSalle2;  // Mémoriser l'audio actif (Salle 2)
    });

    // Lors de la mise en pause de la vidéo
    video.addEventListener("pause", function() {
        // Mémoriser l'audio actif au moment de la pause
        if (!audioSalle1.muted) {
            audioActif = audioSalle1;  // Si l'audio de la salle 1 était actif
        } else {
            audioActif = audioSalle2;  // Si l'audio de la salle 2 était actif
        }

        // Mettre en pause les deux audios
        audioSalle1.pause();
        audioSalle2.pause();
    });

    // Lors de la reprise de la vidéo (après pause)
    video.addEventListener("play", function() {
        if (audioActif) {
            audioActif.play();  // Reprendre l'audio actif
            audioActif.currentTime = video.currentTime;  // Synchroniser l'audio avec la vidéo
        }
    });

    // Synchroniser la position de l'audio avec celle de la vidéo
    video.addEventListener("timeupdate", function() {
        var currentTime = video.currentTime;
        audioSalle1.currentTime = currentTime;
        audioSalle2.currentTime = currentTime;
    });

    // Lorsqu'on se déplace dans la vidéo, on reprend l'audio actif
    video.addEventListener("seeked", function() {
        if (audioActif) {
            audioActif.currentTime = video.currentTime;  // Synchroniser l'audio
            audioActif.play();  // Relancer l'audio actif
        }
    });

    // Bascule entre l'audio de la première et de la seconde salle
    document.getElementById("btnBascule").addEventListener("click", function() {
        if (audioSalle1.muted) {
            // Si l'audio de la salle 1 est muet, on le rend audible et mute celui de la salle 2
            audioSalle1.muted = false;
            audioSalle2.muted = true;
            audioActif = audioSalle1;  // Mémoriser l'audio actif
        } else {
            // Si l'audio de la salle 2 est muet, on le rend audible et mute celui de la salle 1
            audioSalle1.muted = true;
            audioSalle2.muted = false;
            audioActif = audioSalle2;  // Mémoriser l'audio actif
        }
    });
</script>

</body>
</html>
