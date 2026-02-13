<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy Valentine's Day, Sayang!</title>
    <style>
        /* (Sama seperti kode sebelumnya, saya potong untuk singkat – salin lengkap dari sebelumnya) */
        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(45deg, #ff69b4, #ffb6c1, #ff1493);
            background-size: 400% 400%;
            animation: gradientShift 10s ease infinite;
            color: white;
            text-align: center;
            margin: 0;
            padding: 0;
            overflow-x: hidden;
        }
        @keyframes gradientShift {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }
        .container {
            padding: 50px;
            max-width: 900px;
            margin: 0 auto;
        }
        h1 {
            font-size: 3em;
            margin-bottom: 20px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
            animation: fadeIn 2s;
        }
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        p {
            font-size: 1.5em;
            line-height: 1.6;
            animation: slideUp 2s;
        }
        @keyframes slideUp {
            from { transform: translateY(50px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }
        .heart {
            font-size: 5em;
            color: red;
            animation: pulse 1s infinite, bounce 2s infinite;
        }
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }
        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
            40% { transform: translateY(-10px); }
            60% { transform: translateY(-5px); }
        }
        .slideshow {
            position: relative;
            max-width: 500px;
            margin: 20px auto;
            overflow: hidden;
            border-radius: 10px;
            box-shadow: 0 0 20px rgba(0,0,0,0.3);
        }
        .slideshow img {
            width: 100%;
            display: none;
            transition: opacity 1s ease-in-out;
        }
        .slideshow img.active {
            display: block;
        }
        .button {
            display: inline-block;
            padding: 15px 30px;
            background: linear-gradient(45deg, #ff1493, #c71585);
            color: white;
            text-decoration: none;
            border-radius: 25px;
            margin: 10px;
            font-size: 1.2em;
            transition: transform 0.3s, box-shadow 0.3s;
            cursor: pointer;
            border: none;
        }
        .button:hover {
            transform: scale(1.1);
            box-shadow: 0 0 15px rgba(255,20,147,0.5);
        }
        .form {
            margin-top: 30px;
            background: rgba(255,255,255,0.1);
            padding: 20px;
            border-radius: 10px;
            backdrop-filter: blur(10px);
        }
        .form input, .form textarea {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: none;
            border-radius: 5px;
            font-size: 1em;
        }
        .form button {
            width: 100%;
        }
        .messages {
            margin-top: 20px;
            text-align: left;
            background: rgba(0,0,0,0.2);
            padding: 10px;
            border-radius: 5px;
            max-height: 200px;
            overflow-y: auto;
        }
        .confetti {
            position: absolute;
            width: 10px;
            height: 10px;
            background: #ff1493;
            animation: fall 3s linear infinite;
        }
        @keyframes fall {
            to { transform: translateY(100vh); }
        }
        audio {
            margin-top: 20px;
            width: 100%;
            max-width: 300px;
        }
    </style>
</head>
<body onload="startConfetti(); startSlideshow();">
    <div class="container">
        <h1>Happy Valentine's Day, [Shofy Ismawati]!</h1>
        <div class="heart">❤</div>
        <p>Kamu adalah cahaya dalam hidupku. Setiap hari bersamamu adalah petualangan yang indah. Aku mencintaimu lebih dari kata-kata bisa ungkapkan. Terima kasih telah menjadi bagian dari hidupku. 💕</p>
        <p>Ini adalah hadiah kecil dariku untukmu. Mari kita buat kenangan baru hari ini!</p>
        
        <!-- Slideshow Foto -->
        <div class="slideshow">
            <img src="https://probable-amber-pkz6gmdty9.edgeone.app/IMG-20260209-WA0066.jpg" alt="Foto 1" class="active">
            <img src="https://deaf-apricot-m4peiiwzdn.edgeone.app/IMG-20260202-WA0015.jpg" alt="Foto 2">
            <img src="https://administrative-jade-esrjjt7vxd.edgeone.app/IMG-20260214-WA0000.jpg" alt="Foto 3">
        </div>
        
        <!-- Kontrol Musik -->
        <audio id="music" controls loop>
            <source src="https://strong-plum-xz7gfgmm0v.edgeone.app/playback.mp3" type="audio/mpeg">
            Browser kamu tidak mendukung audio.
        </audio>
        
        <!-- Tombol Interaktif -->
        <button class="button" onclick="showMessage()">Tampilkan Pesan Khusus</button>
        <button class="button" onclick="toggleMusic()">Play/Pause Musik</button>
        
        <!-- Formulir Pesan Rahasia -->
        <div class="form">
            <h2>Tulis Pesan Balik untukku 💌</h2>
            <input type="text" id="name" placeholder="Nama kamu">
            <textarea id="message" placeholder="Pesan cinta kamu..."></textarea>
            <button class="button" onclick="saveMessage()">Kirim Pesan</button>
        </div>
        
        <!-- Daftar Pesan -->
        <div class="messages" id="messagesList">
            <h3>Pesan dari Pacar:</h3>
        </div>
    </div>

    <script>
        // Animasi Confetti
        function startConfetti() {
            for (let i = 0; i < 100; i++) {
                const confetti = document.createElement('div');
                confetti.className = 'confetti';
                confetti.style.left = Math.random() * 100 + 'vw';
                confetti.style.animationDelay = Math.random() * 3 + 's';
                confetti.style.background = `hsl(${Math.random() * 360}, 100%, 50%)`;
                document.body.appendChild(confetti);
                setTimeout(() => confetti.remove(), 3000);
            }
        }

        // Slideshow Foto
        let slideIndex = 0;
        function startSlideshow() {
            const slides = document.querySelectorAll('.slideshow img');
            setInterval(() => {
                slides[slideIndex].classList.remove('active');
                slideIndex = (slideIndex + 1) % slides.length;
                slides[slideIndex].classList.add('active');
            }, 3000); // Ganti gambar setiap 3 detik
        }

        // Kontrol Musik
        function toggleMusic() {
            const audio = document.getElementById('music');
            if (audio.paused) {
                audio.play();
            } else {
                audio.pause();
            }
        }

        // Pesan Khusus
        function showMessage() {
            alert('Kamu adalah segalanya bagiku! Aku cinta kamu selamanya. ❤️');
        }

        // Simpan Pesan ke LocalStorage
        function saveMessage() {
            const name = document.getElementById('name').value.trim();
            const message = document.getElementById('message').value.trim();
            if (name && message) {
                const messages = JSON.parse(localStorage.getItem('valentineMessages') || '[]');
                messages.push({ name, message, date: new Date().toLocaleString() });
                localStorage.setItem('valentineMessages', JSON.stringify(messages));
                displayMessages();
                document.getElementById('name').value = '';
                document.getElementById('message').value = '';
                alert('Pesan tersimpan! Terima kasih, sayang. 💕');
            } else {
                alert('Isi nama dan pesan dulu ya! Jangan kosong.');
            }
        }

        // Tampilkan Pesan (dengan pesan default jika kosong)
        function displayMessages() {
            const messages = JSON.parse(localStorage.getItem('valentineMessages') || '[]');
            const list = document.getElementById('messagesList');
            list.innerHTML = '<h3>Pesan dari Pacar:</h3>';
            if (messages.length === 0) {
                list.innerHTML += '<p style="color: #ffb6c1;">Belum ada pesan. Isi form di atas dan kirim ya! 💌</p>';
            } else {
                messages.forEach(msg => {
                    list.innerHTML += `<p><strong>${msg.name}</strong> (${msg.date}): ${msg.message}</p>`;
                });
            }
        }
        displayMessages(); // Load pesan saat halaman buka
    </script>
</body>
</html>
