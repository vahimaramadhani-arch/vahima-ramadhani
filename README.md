# vahima-ramadhani<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Adopsi Aku Please! 🐾</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background: linear-gradient(135deg, #ffe5ec, #ffc2d1);
            overflow: hidden;
        }

        .container {
            background: rgba(255, 255, 255, 0.9);
            padding: 30px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(251, 111, 146, 0.2);
            text-align: center;
            max-width: 400px;
            width: 90%;
            border: 3px solid #ffb3c6;
            position: relative;
        }

        .sticker {
            font-size: 80px;
            margin-bottom: 20px;
            display: inline-block;
            transition: transform 0.3s;
        }

        .sticker:hover {
            transform: scale(1.1) rotate(5deg);
        }

        h1 {
            color: #ff477e;
            font-size: 24px;
            margin-bottom: 10px;
        }

        p {
            color: #6c757d;
            font-size: 16px;
            margin-bottom: 30px;
        }

        .btn-container {
            display: flex;
            justify-content: center;
            gap: 20px;
            height: 50px;
            position: relative;
        }

        button {
            padding: 12px 30px;
            font-size: 16px;
            font-weight: bold;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.2s ease;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }

        #btn-oke {
            background-color: #ff477e;
            color: white;
        }

        #btn-oke:hover {
            background-color: #ff7096;
            transform: scale(1.05);
        }

        #btn-tidak {
            background-color: #6c757d;
            color: white;
            position: absolute;
            /* Inisialisasi posisi awal tombol tidak di sebelah kanan */
            right: 60px; 
        }

        /* Kelas untuk menyembunyikan elemen */
        .hidden {
            display: none;
        }

        .pesan-sukses {
            color: #ff477e;
            animation: popIn 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        @keyframes popIn {
            0% { transform: scale(0); }
            100% { transform: scale(1); }
        }
    </style>
</head>
<body>

    <div class="container">
        <div id="konten-tanya">
            <div class="sticker" id="sticker-cat">🐱</div>
            <h1 id="judul">Halo Manusia Bumi!</h1>
            <p id="deskripsi">Mau kah kamu mengadopsi dan memberiku makan setiap hari? 🥺</p>
            
            <div class="btn-container">
                <button id="btn-oke">Oke</button>
                <button id="btn-tidak">Tidak</button>
            </div>
        </div>

        <div id="konten-sukses" class="hidden pesan-sukses">
            <div class="sticker">😸🎉</div>
            <h1>Yeeayyy, Terima Kasih!</h1>
            <p>Sekarang kita berteman selamanya! Siapkan makanan yang banyak ya! ❤️</p>
        </div>
    </div>

    <script>
        const btnOke = document.getElementById('btn-oke');
        const btnTidak = document.getElementById('btn-tidak');
        const kontenTanya = document.getElementById('konten-tanya');
        const kontenSukses = document.getElementById('konten-sukses');
        const stickerCat = document.getElementById('sticker-cat');

        // Ganti stiker berkala biar makin lucu
        const emojis = ['🐱', '😸', '🙀', '😿', '🥺'];
        setInterval(() => {
            // Hanya ganti emoji jika konten tanya masih aktif
            if (!kontenTanya.classList.contains('hidden')) {
                const randomEmoji = emojis[Math.floor(Math.random() * emojis.length)];
                // Cegah ganti emoji jika tombol 'Tidak' sedang dikejar (biar fokus ke emoji panik)
                if (stickerCat.innerText !== '🙀') {
                    stickerCat.innerText = randomEmoji;
                }
            }
        }, 3000);

        // Fungsi ketika tombol 'Tidak' didekati atau diklik
        function pindahTombol() {
            // Ubah stiker jadi panik saat tombol melarikan diri
            stickerCat.innerText = '🙀';

            // Dapatkan ukuran window browser
            const padding = 20;
            const batasKanan = window.innerWidth - btnTidak.offsetWidth - padding;
            const batasBawah = window.innerHeight - btnTidak.offsetHeight - padding;

            // Hitung posisi acak di seluruh layar browser
            const randomX = Math.max(padding, Math.floor(Math.random() * batasKanan));
            const randomY = Math.max(padding, Math.floor(Math.random() * batasBawah));

            // Ubah posisi tombol menjadi fixed agar bisa bebas pindah ke mana saja di layar
            btnTidak.style.position = 'fixed';
            btnTidak.style.left = randomX + 'px';
            btnTidak.style.top = randomY + 'px';
        }

        // Kejadian saat pointer mouse mendekati tombol (untuk PC)
        btnTidak.addEventListener('mouseenter', pindahTombol);
        
        // Kejadian saat tombol disentuh (untuk HP/Touchscreen)
        btnTidak.addEventListener('touchstart', (e) => {
            e.preventDefault(); // Mencegah klik bawaan
            pindahTombol();
        });

        // Ketika tombol 'Oke' diklik
        btnOke.addEventListener('click', () => {
            kontenTanya.classList.add('hidden');
            kontenSukses.classList.remove('hidden');
        });
    </script>
</body>
</html>
