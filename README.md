
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Calculatrice de Stères de Bois</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f0f0f0;
      color: #333;
      padding: 20px;
      max-width: 600px;
      margin: auto;
    }
    h1 {
      text-align: center;
    }
    input, select, button {
      display: block;
      width: 100%;
      padding: 10px;
      margin: 12px 0;
      font-size: 16px;
    }
    #resultat {
      font-size: 18px;
      font-weight: bold;
      margin-top: 20px;
      padding: 15px;
      background-color: #dff0d8;
      border-left: 5px solid #3c763d;
    }
  </style>
</head>
<body>

  <h1>🪵 Calculatrice de Stères</h1>

  <label for="longueur">Longueur du tas (m)</label>
  <input type="number" id="longueur" placeholder="ex : 6" step="0.01">

  <label for="hauteur">Hauteur du tas (m)</label>
  <input type="number" id="hauteur" placeholder="ex : 1.7" step="0.01">

  <label for="buches">Longueur des bûches (cm)</label>
  <select id="buches">
    <option value="100">100 cm</option>
    <option value="50" selected>50 cm</option>
    <option value="33">33 cm</option>
    <option value="25">25 cm</option>
  </select>

  <button onclick="calculerSteres()">Calculer</button>

  <div id="resultat"></div>

  <script>
    function getCoefficient(bucheLength) {
      switch (parseInt(bucheLength)) {
        case 100: return 1.00;
        case 50: return 1.25;
        case 33: return 1.43;
        case 25: return 1.67;
        default: return 1.00;
      }
    }

    function calculerSteres() {
      const longueur = parseFloat(document.getElementById("longueur").value);
      const hauteur = parseFloat(document.getElementById("hauteur").value);
      const bucheLength = parseFloat(document.getElementById("buches").value) / 100;

      if (isNaN(longueur) || isNaN(hauteur)) {
        document.getElementById("resultat").innerText = "❗ Veuillez entrer des dimensions valides.";
        return;
      }

      const volumeApparent = longueur * hauteur * bucheLength;
      const coefficient = getCoefficient(document.getElementById("buches").value);
      const stere = volumeApparent * coefficient;

      document.getElementById("resultat").innerHTML =
        `📏 Volume apparent : <strong>${volumeApparent.toFixed(2)} m³</strong><br>` +
        `🪵 Stères estimés : <strong>${stere.toFixed(2)} stères</strong>`;
    }
  </script>
</body>
</html>
