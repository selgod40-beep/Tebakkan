<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<title>Game Tebak-Tebakan 100 Soal</title>

<style>
body {
    font-family: Arial, sans-serif;
    background-image: linear-gradient(to bottom, #f2f2f2, #cccccc);
    background-attachment: fixed;
    background-size: cover;
}

.container {
    width: 80%;
    margin: 40px auto;
    padding: 20px;
    background-color: #fff;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0,0,0,0.1);
    text-align: center;
}

#soal {
    font-size: 22px;
    margin-bottom: 15px;
}

input {
    padding: 10px;
    font-size: 16px;
    width: 60%;
    border-radius: 5px;
    border: 1px solid #ccc;
}

button {
    padding: 10px 20px;
    font-size: 16px;
    background-color: #4CAF50;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    margin-top: 10px;
}

button:hover {
    background-color: #3e8e41;
}

#hasil, #skor {
    margin-top: 10px;
    font-size: 18px;
}
</style>
</head>
<body>

<div class="container">
    <h1>Game Tebak-Tebakan</h1>
    <div id="soal">Tekan mulai untuk bermain</div>
    <input id="jawaban" type="text" placeholder="Masukkan jawaban">
    <br>
    <button id="cek">Cek</button>
    <p id="hasil"></p>
    <p id="skor">Skor: 0</p>
    <button id="mulai">Tekan Enter untuk Memulai</button>
</div>

<script>
const soal = [
{ pertanyaan: "Apa yang punya gigi tapi tidak bisa makan?", jawaban: "sisir" },
{ pertanyaan: "Apa yang punya mata tapi tidak bisa melihat?", jawaban: "jarum" },
{ pertanyaan: "Apa yang selalu naik tapi tidak pernah turun?", jawaban: "umur" },
{ pertanyaan: "Apa yang makin dipotong makin panjang?", jawaban: "jalan" },
{ pertanyaan: "Apa yang kalau dibuang justru berguna?", jawaban: "jangkar" },
{ pertanyaan: "Apa yang bisa berjalan tanpa kaki?", jawaban: "air" },
{ pertanyaan: "Apa yang punya tangan tapi tidak bisa memegang?", jawaban: "jam" },
{ pertanyaan: "Apa yang punya leher tapi tidak punya kepala?", jawaban: "botol" },
{ pertanyaan: "Apa yang selalu mengikuti kita tapi tidak menyentuh?", jawaban: "bayangan" },
{ pertanyaan: "Apa yang selalu basah saat mengeringkan?", jawaban: "handuk" },
{ pertanyaan: "Apa yang punya banyak lubang tapi menahan air?", jawaban: "spons" },
{ pertanyaan: "Apa yang semakin tua semakin kecil?", jawaban: "sabun" },
{ pertanyaan: "Apa yang bisa pecah tanpa dijatuhkan?", jawaban: "janji" },
{ pertanyaan: "Apa yang punya banyak halaman tapi bukan rumah?", jawaban: "buku" },
{ pertanyaan: "Apa yang selalu datang tapi tidak pernah tiba?", jawaban: "besok" },
{ pertanyaan: "Apa yang punya banyak kunci tapi tak bisa buka pintu?", jawaban: "piano" },
{ pertanyaan: "Apa yang bisa berlari tanpa kaki?", jawaban: "air" },
{ pertanyaan: "Apa yang selalu ada di tengah malam?", jawaban: "a" },
{ pertanyaan: "Apa yang selalu ada di tengah laut?", jawaban: "u" },
{ pertanyaan: "Apa yang tidak pernah tidur?", jawaban: "matahari" },
{ pertanyaan: "Apa yang semakin dibagi semakin banyak?", jawaban: "ilmu" },
{ pertanyaan: "Apa yang punya kepala tapi tidak punya otak?", jawaban: "paku" },
{ pertanyaan: "Apa yang punya kaki tapi tidak berjalan?", jawaban: "meja" },
{ pertanyaan: "Apa yang bisa terbang tanpa sayap?", jawaban: "waktu" },
{ pertanyaan: "Apa yang tidak bisa dilihat tapi bisa didengar?", jawaban: "suara" },
{ pertanyaan: "Apa yang punya rumah tapi tidak tinggal?", jawaban: "siput" },
{ pertanyaan: "Apa yang semakin diisi semakin ringan?", jawaban: "balon" },
{ pertanyaan: "Apa yang bisa berdiri tanpa kaki?", jawaban: "tiang" },
{ pertanyaan: "Apa yang tidak bisa ditahan lama?", jawaban: "napas" },
{ pertanyaan: "Apa yang selalu ada di atas kepala?", jawaban: "langit" },
{ pertanyaan: "Apa yang bisa dimakan tapi bukan makanan?", jawaban: "hati" },
{ pertanyaan: "Apa yang selalu bergerak tapi tidak berjalan?", jawaban: "jam" },
{ pertanyaan: "Apa yang semakin ditarik semakin pendek?", jawaban: "rokok" },
{ pertanyaan: "Apa yang punya banyak rambut tapi tidak punya kepala?", jawaban: "sapu" },
{ pertanyaan: "Apa yang bisa masuk air tapi tidak basah?", jawaban: "cahaya" },
{ pertanyaan: "Apa yang selalu mengikutimu saat terang?", jawaban: "bayangan" },
{ pertanyaan: "Apa yang punya wajah tapi bukan manusia?", jawaban: "jam" },
{ pertanyaan: "Apa yang selalu berputar tapi tidak ke mana-mana?", jawaban: "kipas" },
{ pertanyaan: "Apa yang punya banyak warna tapi tidak berbicara?", jawaban: "pelangi" },
{ pertanyaan: "Apa yang bisa mengisi ruangan tanpa mengambil tempat?", jawaban: "cahaya" },
{ pertanyaan: "Apa yang tidak pernah basah walau di air?", jawaban: "bayangan" },
{ pertanyaan: "Apa yang selalu ada di akhir cerita?", jawaban: "titik" },
{ pertanyaan: "Apa yang punya banyak kota tapi tidak ada rumah?", jawaban: "peta" },
{ pertanyaan: "Apa yang bisa melompat tanpa kaki?", jawaban: "bola" },
{ pertanyaan: "Apa yang selalu ada di antara siang dan malam?", jawaban: "dan" },
{ pertanyaan: "Apa yang tidak bisa bergerak tapi bisa bepergian?", jawaban: "surat" },
{ pertanyaan: "Apa yang semakin tinggi semakin dingin?", jawaban: "gunung" },
{ pertanyaan: "Apa yang selalu ada di tengah kata kertas?", jawaban: "r" },
{ pertanyaan: "Apa yang bisa berubah bentuk tapi tetap air?", jawaban: "es" },
{ pertanyaan: "Apa yang bisa hancur tanpa disentuh?", jawaban: "kepercayaan" }
];

// otomatis acak soal
soal.sort(() => Math.random() - 0.5);

let skor = 0;
let currentSoal = 0;
let gameMulai = false;

const soalDiv = document.getElementById("soal");
const jawabanInput = document.getElementById("jawaban");
const hasil = document.getElementById("hasil");
const skorText = document.getElementById("skor");
const mulaiBtn = document.getElementById("mulai");

mulaiBtn.addEventListener("click", mulaiGame);
document.getElementById("cek").addEventListener("click", cekJawaban);

document.addEventListener("keydown", function(e) {
    if (e.key === "Enter") {
        if (!gameMulai) mulaiGame();
        else cekJawaban();
    }
});

function mulaiGame() {
    gameMulai = true;
    skor = 0;
    currentSoal = 0;
    skorText.innerText = "Skor: 0";
    hasil.innerText = "";
    mulaiBtn.style.display = "none";
    tampilkanSoal();
}

function tampilkanSoal() {
    soalDiv.innerText = soal[currentSoal].pertanyaan;
}

function cekJawaban() {
    if (!gameMulai) return;

    const userJawab = jawabanInput.value.toLowerCase();
    const s = soal[currentSoal];

    if (userJawab === s.jawaban.toLowerCase()) {
        hasil.innerText = "Benar!";
        skor++;
        skorText.innerText = "Skor: " + skor;
    } else {
        hasil.innerText = "Salah! Jawaban: " + s.jawaban;
    }

    currentSoal++;

    if (currentSoal >= soal.length) {
        soalDiv.innerText = "Game selesai! Skor akhir: " + skor;
        gameMulai = false;
        mulaiBtn.style.display = "block";
    } else {
        tampilkanSoal();
    }

    jawabanInput.value = "";
}
</script>

</body>
</html>
