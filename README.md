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
        /* Masquer les lecteurs audio */
        .audio-container iframe {
            display: none;
        }
    </style>
</head>
<body>

<h1 class="titre-1">Fumée Omnisciente, Mirage Onirique | Résidence de création, janvier 2025, Bain Mathieu</h1>

<div class="video-container">
    <iframe id="video" src="https://www.youtube.com/embed/fm00cFcoJM8?enablejsapi=1" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
    <button id="btnBascule" class="btn-video">Audio salle de droite</button>
</div>

<div class="audio-container">
    <!-- Audio Salle 1 (SoundCloud) -->
    <iframe id="audioSalle1" width="100%" height="166" scrolling="no" frameborder="no" 
        src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/2051283100%3Fsecret_token%3Ds-6d0R4mFbF6v&color=%23ff5500&auto_play=false&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true&visual=false">
    </iframe>
    <!-- Audio Salle 2 (SoundCloud) -->
    <iframe id="audioSalle2" width="100%" height="166" scrolling="no" frameborder="no" 
        src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/1742214405%3Fsecret_token%3Ds-UuYn7gHeGzR&color=%23ff5500&auto_play=false&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true&visual=false">
    </iframe>
</div>

<script src="https://w.soundcloud.com/player/api.js"></script>

<script>
    var btnBascule = document.getElementById("btnBascule");
    var audioActif;
    var player;
    
    // Initialisation des lecteurs audio SoundCloud
    var scPlayerSalle1;
    var scPlayerSalle2;

    window.onload = function() {
        scPlayerSalle1 = SC.Widget("audioSalle1");
        scPlayerSalle2 = SC.Widget("audioSalle2");
        
        // Désactiver la lecture automatique au début
        scPlayerSalle1.bind(SC.Widget.Events.READY, function() {
            scPlayerSalle1.pause();
        });

        scPlayerSalle2.bind(SC.Widget.Events.READY, function() {
            scPlayerSalle2.pause();
        });

        // Initialisation de l'audio actif
        audioActif = scPlayerSalle2;
    };

    // Fonction d'initialisation de l'API YouTube
    function onYouTubePlayerAPIReady() {
        player = new YT.Player('video', {
            events: {
                'onStateChange': onPlayerStateChange
            }
        });
    }

    // Quand l'état de la vidéo change (lecture, pause, etc.)
    function onPlayerStateChange(event) {
        if (event.data == YT.PlayerState.PLAYING) {
            if (audioActif) {
                audioActif.play();
            }
        } else if (event.data == YT.PlayerState.PAUSED) {
            if (audioActif) {
                audioActif.pause();
            }
        }
    }

    // Bascule entre les salles audio
    btnBascule.addEventListener("click", function() {
        if (audioActif === scPlayerSalle1) {
            audioActif = scPlayerSalle2;
            btnBascule.textContent = "Audio salle de droite";
            btnBascule.classList.remove("btn-salle1");
            btnBascule.classList.add("btn-salle2");
        } else {
            audioActif = scPlayerSalle1;
            btnBascule.textContent = "Audio salle de gauche";
            btnBascule.classList.remove("btn-salle2");
            btnBascule.classList.add("btn-salle1");
        }

        // Synchroniser l'audio avec la vidéo
        if (player.getPlayerState() === YT.PlayerState.PLAYING) {
            audioActif.play();
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
