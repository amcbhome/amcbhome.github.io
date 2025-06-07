---
layout: page
title: "Portfolio Statistics Calculator"
---

# Portfolio Statistics Calculator

<form id="calc-form">
  <h3>Enter 5 values for X (up to 2 decimal places):</h3>
  <input type="number" step="0.01" id="x1" required>
  <input type="number" step="0.01" id="x2" required>
  <input type="number" step="0.01" id="x3" required>
  <input type="number" step="0.01" id="x4" required>
  <input type="number" step="0.01" id="x5" required>

  <h3>Enter 5 values for Y (up to 2 decimal places):</h3>
  <input type="number" step="0.01" id="y1" required>
  <input type="number" step="0.01" id="y2" required>
  <input type="number" step="0.01" id="y3" required>
  <input type="number" step="0.01" id="y4" required>
  <input type="number" step="0.01" id="y5" required>

  <h3>Enter weights for X and Y (must add up to 1):</h3>
  <input type="number" step="0.01" id="wX" placeholder="Weight of X (e.g., 0.6)" required>
  <input type="number" step="0.01" id="wY" placeholder="Weight of Y (e.g., 0.4)" required>

  <br><br>
  <button type="submit">Calculate Portfolio Statistics</button>
</form>

<p id="result"></p>

<script>
document.getElementById('calc-form').addEventListener('submit', function(e) {
  e.preventDefault();

  // Get X and Y values
  const x = [1,2,3,4,5].map(i => parseFloat(document.getElementById('x' + i).value));
  const y = [1,2,3,4,5].map(i => parseFloat(document.getElementById('y' + i).value));

  // Get weights
  const wX = parseFloat(document.getElementById('wX').value);
  const wY = parseFloat(document.getElementById('wY').value);

  if (wX + wY !== 1) {
    document.getElementById('result').innerHTML = "<b style='color:red;'>Weights must add up to 1.</b>";
    return;
  }

  // Means
  const avgX = x.reduce((a,b) => a + b, 0) / x.length;
  const avgY = y.reduce((a,b) => a + b, 0) / y.length;

  // Population std dev
  const stdDevX = Math.sqrt(x.reduce((sum, val) => sum + Math.pow(val - avgX, 2), 0) / x.length);
  const stdDevY = Math.sqrt(y.reduce((sum, val) => sum + Math.pow(val - avgY, 2), 0) / y.length);

  // Pearson r
  let numerator = 0, denomX = 0, denomY = 0;
  for (let i = 0; i < x.length; i++) {
    const dx = x[i] - avgX;
    const dy = y[i] - avgY;
    numerator += dx * dy;
    denomX += dx * dx;
    denomY += dy * dy;
  }
  const r = numerator / Math.sqrt(denomX * denomY);

  // Portfolio expected return
  const portMean = wX * avgX + wY * avgY;

  // Portfolio variance & std dev
  const portVar = Math.pow(wX * stdDevX, 2) + Math.pow(wY * stdDevY, 2) + 2 * wX * wY * stdDevX * stdDevY * r;
  const portStdDev = Math.sqrt(portVar);

  // Display results
  document.getElementById('result').innerHTML =
    "<b>Mean of X:</b> " + avgX.toFixed(2) + "<br>" +
    "<b>Mean of Y:</b> " + avgY.toFixed(2) + "<br>" +
    "<b>Population Std Dev of X:</b> " + stdDevX.toFixed(2) + "<br>" +
    "<b>Population Std Dev of Y:</b> " + stdDevY.toFixed(2) + "<br>" +
    "<b>Pearson Correlation (r):</b> " + r.toFixed(4) + "<br><br>" +
    "<b>Portfolio Expected Return:</b> " + portMean.toFixed(2) + "<br>" +
    "<b>Portfolio Std Dev (Risk):</b> " + portStdDev.toFixed(2);
});
</script>

