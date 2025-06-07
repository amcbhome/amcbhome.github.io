---
layout: page
title: "X and Y Statistical Calculator"
---

# X and Y Statistical Calculator

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

  <br><br>
  <button type="submit">Calculate Statistics</button>
</form>

<p id="result"></p>

<script>
document.getElementById('calc-form').addEventListener('submit', function(e) {
  e.preventDefault();

  // Get X values
  const x = [
    parseFloat(document.getElementById('x1').value),
    parseFloat(document.getElementById('x2').value),
    parseFloat(document.getElementById('x3').value),
    parseFloat(document.getElementById('x4').value),
    parseFloat(document.getElementById('x5').value)
  ];

  // Get Y values
  const y = [
    parseFloat(document.getElementById('y1').value),
    parseFloat(document.getElementById('y2').value),
    parseFloat(document.getElementById('y3').value),
    parseFloat(document.getElementById('y4').value),
    parseFloat(document.getElementById('y5').value)
  ];

  // Calculate means
  const avgX = x.reduce((sum, val) => sum + val, 0) / x.length;
  const avgY = y.reduce((sum, val) => sum + val, 0) / y.length;

  // Calculate population standard deviation
  const stdDevX = Math.sqrt(x.reduce((sum, val) => sum + Math.pow(val - avgX, 2), 0) / x.length);
  const stdDevY = Math.sqrt(y.reduce((sum, val) => sum + Math.pow(val - avgY, 2), 0) / y.length);

  // Calculate Pearson correlation coefficient
  let numerator = 0;
  let denomX = 0;
  let denomY = 0;
  for (let i = 0; i < x.length; i++) {
    const dx = x[i] - avgX;
    const dy = y[i] - avgY;
    numerator += dx * dy;
    denomX += dx * dx;
    denomY += dy * dy;
  }
  const denominator = Math.sqrt(denomX * denomY);
  const r = numerator / denominator;

  // Display results
  document.getElementById('result').innerHTML =
    "<b>Mean of X:</b> " + avgX.toFixed(2) + "<br>" +
    "<b>Mean of Y:</b> " + avgY.toFixed(2) + "<br>" +
    "<b>Population Standard Deviation of X:</b> " + stdDevX.toFixed(2) + "<br>" +
    "<b>Population Standard Deviation of Y:</b> " + stdDevY.toFixed(2) + "<br>" +
    "<b>Pearson Correlation (r):</b> " + r.toFixed(4);
});
</script>

