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
            font-size: 16px;  /* Ajuste la taille ici comme tu le souhaites */
            font-weight: bold;
            color: #333;  /* Facultatif : change la couleur si nécessaire */
        }
    </style>
</head>
<body>

    <h1>Fumée Omnisciente, Mirage Onirique</h1>

    <h1>Résidence de création, janvier 2025, Bain Mathieu</h1>

    <!-- Vidéo divisée en deux (les deux salles) -->
    <video id="video" controls autoplay>
        <source src="https://www.dropbox.com/scl/fi/vn856dku4ckgm35azhbz1/Fumee-Omnisciente-Mirage-Onirique02.mp4?rlkey=khuru1f6c5woeclemz1ai9rlz&st=pksoqe29&raw=1" type="video/mp4">    
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
        document.getElementById("video").addEventListener("play", function() {
            // Lors du démarrage de la vidéo, les deux pistes audio sont lancées et non muettes
            var audioSalle1 = document.getElementById("audioSalle1");
            var audioSalle2 = document.getElementById("audioSalle2");

            // Variables pour mémoriser l'audio actif
            var audioActif = audioSalle2;

            audioSalle1.play();
            audioSalle2.play();
            audioSalle1.muted = true;  // D'abord, on mute l'audio de la salle 1, donc seul l'audio de la salle 2 est audible
            audioActif = audioSalle2;  // Mémoriser l'audio actif
        });

        document.getElementById("btnBascule").addEventListener("click", function() {
            var audioSalle1 = document.getElementById("audioSalle1");
            var audioSalle2 = document.getElementById("audioSalle2");

            // Mettre l'audio en pause quand la vidéo est mise en pause
        document.getElementById("video").addEventListener("pause", function() {
            var audioSalle1 = document.getElementById("audioSalle1");
            var audioSalle2 = document.getElementById("audioSalle2");

            audioSalle1.pause();
            audioSalle2.pause();
        });

        // Synchroniser la position de l'audio avec celle de la vidéo
        video.addEventListener("timeupdate", function() {
            var currentTime = video.currentTime;  // Temps actuel de la vidéo
            audioSalle1.currentTime = currentTime;  // Synchroniser l'audio 1
            audioSalle2.currentTime = currentTime;  // Synchroniser l'audio 2
        });

        // Mettre à jour la position de l'audio lorsque l'utilisateur déplace le curseur
        video.addEventListener("seeked", function() {
            var currentTime = video.currentTime;  // Temps actuel après la recherche
            audioSalle1.currentTime = currentTime;  // Synchroniser l'audio 1
            audioSalle2.currentTime = currentTime;  // Synchroniser l'audio 2
            // Restaure l'audio actif avant le déplacement
            if (audioActif === audioSalle1) {
                audioSalle1.muted = false;
                audioSalle2.muted = true;
            } else {
                audioSalle1.muted = true;
                audioSalle2.muted = false;
            }
        });

            // Bascule entre l'audio de la première et de la deuxième salle
            if (audioSalle1.muted) {
                // Si l'audio de la salle 1 est muet, on le rend audible et on mute celui de la salle 2
                audioSalle1.muted = false;
                audioSalle2.muted = true;
                audioActif = audioSalle1;  // Mémoriser l'audio actif après bascule
            } else {
                // Si l'audio de la salle 2 est muet, on le rend audible et on mute celui de la salle 1
                audioSalle1.muted = true;
                audioSalle2.muted = false;
                audioActif = audioSalle2;  // Mémoriser l'audio actif après bascule
            }
        });
    </script>
</body>
</html>
