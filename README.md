<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kalkulator & Grafik Persamaan Lingkaran</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f4f7f6;
            color: #333;
            margin: 0;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        h1 {
            color: #2c3e50;
            text-align: center;
        }
        .container {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
            max-width: 900px;
            width: 100%;
            justify-content: center;
        }
        .card {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
            flex: 1;
            min-width: 300px;
        }
        .input-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            font-weight: bold;
            margin-bottom: 5px;
        }
        input[type="number"] {
            width: 100%;
            padding: 8px;
            box-sizing: border-box;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 16px;
        }
        button {
            width: 100%;
            padding: 10px;
            background-color: #3498db;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
            font-weight: bold;
        }
        button:hover {
            background-color: #2980b9;
        }
        .result-box {
            margin-top: 20px;
            padding: 15px;
            background-color: #eef7fc;
            border-left: 4px solid #3498db;
            border-radius: 4px;
        }
        .result-box p {
            margin: 8px 0;
            font-size: 15px;
        }
        canvas {
            background-color: #fff;
            border: 1px solid #ccc;
            border-radius: 5px;
            display: block;
            margin: 0 auto;
        }
        footer {
            margin-top: 30px;
            font-size: 14px;
            color: #777;
        }
    </style>
</head>
<body>

    <h1>Kalkulator & Visualisasi Persamaan Lingkaran</h1>

    <div class="container">
        <!-- Panel Input & Hasil -->
        <div class="card">
            <h3>Masukkan Parameter Lingkaran</h3>
            <div class="input-group">
                <label for="titikA">Titik Pusat X (a):</label>
                <input type="number" id="titikA" value="2" step="any">
            </div>
            <div class="input-group">
                <label for="titikB">Titik Pusat Y (b):</label>
                <input type="number" id="titikB" value="-1" step="any">
            </div>
            <div class="input-group">
                <label for="jariJari">Jari-jari (r):</label>
                <input type="number" id="jariJari" value="4" min="0.1" step="any">
            </div>
            <button onclick="hitungDanGambar()">Hitung & Gambar Grafik</button>

            <div class="result-box" id="hasil">
                <!-- Hasil perhitungan akan muncul di sini -->
            </div>
        </div>

        <!-- Panel Grafik Kartesius -->
        <div class="card">
            <h3>Grafik Koordinat Kartesius</h3>
            <canvas id="kanvasLingkaran" width="360" height="360"></canvas>
            <p style="text-align: center; font-size: 12px; color: #666; margin-top: 8px;">
                Skala: 1 kotak = 1 satuan (Rentang -10 s/d 10)
            </p>
        </div>
    </div>

    <footer>
        Dibuat untuk pembelajaran Matematika | Di-host dengan GitHub Pages
    </footer>

    <script>
        function formatTanda(angka) {
            if (angka < 0) return `+ ${Math.abs(angka)}`;
            if (angka > 0) return `- ${angka}`;
            return "";
        }

        function formatUmum(angka) {
            if (angka > 0) return `+ ${angka}`;
            if (angka < 0) return `- ${Math.abs(angka)}`;
            return "";
        }

        function hitungDanGambar() {
            const a = parseFloat(document.getElementById('titikA').value) || 0;
            const b = parseFloat(document.getElementById('titikB').value) || 0;
            const r = parseFloat(document.getElementById('jariJari').value);

            if (isNaN(r) || r <= 0) {
                alert("Jari-jari (r) harus lebih besar dari 0!");
                return;
            }

            // 1. Persamaan Baku: (x - a)^2 + (y - b)^2 = r^2
            const rKuadrat = parseFloat((r * r).toFixed(2));
            const bagianX = a === 0 ? "x²" : `(x ${formatTanda(a)})²`;
            const bagianY = b === 0 ? "y²" : `(y ${formatTanda(b)})²`;
            const persBaku = `${bagianX} + ${bagianY} = ${rKuadrat}`;

            // 2. Persamaan Umum: x^2 + y^2 + Ax + By + C = 0
            const A = parseFloat((-2 * a).toFixed(2));
            const B = parseFloat((-2 * b).toFixed(2));
            const C = parseFloat((a * a + b * b - r * r).toFixed(2));

            let persUmum = "x² + y² ";
            if (A !== 0) persUmum += `${formatUmum(A)}x `;
            if (B !== 0) persUmum += `${formatUmum(B)}y `;
            if (C !== 0) persUmum += `${formatUmum(C)} `;
            persUmum += "= 0";

            // 3. Luas dan Keliling
            const luas = (Math.PI * r * r).toFixed(2);
            const keliling = (2 * Math.PI * r).toFixed(2);

            // Tampilkan ke HTML
            document.getElementById('hasil').innerHTML = `
                <p><strong>Titik Pusat:</strong> P(${a}, ${b})</p>
                <p><strong>Persamaan Baku:</strong><br> ${persBaku}</p>
                <p><strong>Persamaan Umum:</strong><br> ${persUmum}</p>
                <p><strong>Luas:</strong> ${luas} satuan luas</p>
                <p><strong>Keliling:</strong> ${keliling} satuan panjang</p>
            `;

            // Gambar di Canvas
            gambarKanvas(a, b, r);
        }

        function gambarKanvas(a, b, r) {
            const canvas = document.getElementById('kanvasLingkaran');
            const ctx = canvas.getContext('2d');
            const lebar = canvas.width;
            const tinggi = canvas.height;
            const pusatX = lebar / 2;
            const pusatY = tinggi / 2;
            const skala = lebar / 20; // Rentang -10 sampai 10 (total 20 unit)

            // Bersihkan kanvas
            ctx.clearRect(0, 0, lebar, tinggi);

            // Gambar grid kotak
            ctx.strokeStyle = "#e0e0e0";
            ctx.lineWidth = 1;
            for (let i = 0; i <= lebar; i += skala) {
                ctx.beginPath();
                ctx.moveTo(i, 0);
                ctx.lineTo(i, tinggi);
                ctx.stroke();

                ctx.beginPath();
                ctx.moveTo(0, i);
                ctx.lineTo(lebar, i);
                ctx.stroke();
            }

            // Gambar Sumbu X dan Y
            ctx.strokeStyle = "#333";
            ctx.lineWidth = 2;
            
            // Sumbu X
            ctx.beginPath();
            ctx.moveTo(0, pusatY);
            ctx.lineTo(lebar, pusatY);
            ctx.stroke();

            // Sumbu Y
            ctx.beginPath();
            ctx.moveTo(pusatX, 0);
            ctx.lineTo(pusatX, tinggi);
            ctx.stroke();

            // Konversi koordinat Kartesius ke koordinat Canvas
            const kanvasA = pusatX + (a * skala);
            const kanvasB = pusatY - (b * skala);
            const kanvasR = r * skala;

            // Gambar Lingkaran
            ctx.strokeStyle = "#e74c3c";
            ctx.lineWidth = 2.5;
            ctx.beginPath();
            ctx.arc(kanvasA, kanvasB, kanvasR, 0, 2 * Math.PI);
            ctx.stroke();

            // Gambar Garis Jari-jari
            ctx.strokeStyle = "#2ecc71";
            ctx.setLineDash([5, 5]);
            ctx.beginPath();
            ctx.moveTo(kanvasA, kanvasB);
            ctx.lineTo(kanvasA + kanvasR, kanvasB);
            ctx.stroke();
            ctx.setLineDash([]); // Reset garis putus-putus

            // Gambar Titik Pusat
            ctx.fillStyle = "#2c3e50";
            ctx.beginPath();
            ctx.arc(kanvasA, kanvasB, 4, 0, 2 * Math.PI);
            ctx.fill();

            // Label Titik Pusat
            ctx.fillStyle = "#2c3e50";
            ctx.font = "bold 12px Arial";
            ctx.fillText(`P(${a},${b})`, kanvasA + 6, kanvasB - 6);
        }

        // Jalankan saat pertama kali halaman dimuat
        window.onload = hitungDanGambar;
    </script>
</body>
</html>
