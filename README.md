# Aplikasi-Statiska-Regresi-Michelle-Kimora
index.html
<!DOCTYPE html>
<html>
<head>
  <title>Aplikasi Statistika Regresi</title>
  <meta charset="UTF-8" />
</head>
<body>
  <h1>Aplikasi Statistika Regresi</h1>
  <p>Masukkan data X dan Y (pisahkan dengan koma):</p>

  <label>X: </label><br>
  <input type="text" id="xInput" placeholder="Contoh: 1,2,3,4"><br><br>

  <label>Y: </label><br>
  <input type="text" id="yInput" placeholder="Contoh: 3,5,7,9"><br><br>

  <label>Nilai X yang ingin diprediksi:</label><br>
  <input type="number" id="xPred" placeholder="Misalnya 5"><br><br>

  <button onclick="hitung()">Hitung Regresi</button>

  <h3>Hasil:</h3>
  <div id="output"></div>

  <script>
    function hitung() {
      try {
        const x = document.getElementById("xInput").value.split(',').map(Number);
        const y = document.getElementById("yInput").value.split(',').map(Number);
        const xPred = parseFloat(document.getElementById("xPred").value);

        if (x.length !== y.length) {
          document.getElementById("output").innerHTML = "⚠️ Data X dan Y harus berjumlah sama.";
          return;
        }

        const n = x.length;
        const sumX = x.reduce((a, b) => a + b, 0);
        const sumY = y.reduce((a, b) => a + b, 0);
        const sumXY = x.reduce((sum, xi, i) => sum + xi * y[i], 0);
        const sumX2 = x.reduce((sum, xi) => sum + xi * xi, 0);

        const slope = (n * sumXY - sumX * sumY) / (n * sumX2 - sumX * sumX);
        const intercept = (sumY - slope * sumX) / n;
        const yPred = slope * xPred + intercept;

        document.getElementById("output").innerHTML =
          `Persamaan regresi: <b>y = ${slope.toFixed(2)}x + ${intercept.toFixed(2)}</b><br>` +
          `Prediksi untuk x = ${xPred}: <b>y = ${yPred.toFixed(2)}</b>`;
      } catch (e) {
        document.getElementById("output").innerHTML = "⚠️ Terjadi kesalahan perhitungan.";
      }
    }
  </script>
</body>
</html>
