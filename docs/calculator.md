---
layout: page
title: "X and Y Average & Correlation Calculator"
---

# X and Y Average & Correlation Calculator

<form id="calc-form">
  <h3>Enter 5 values for X:</h3>
  <input type="number" id="x1" required>
  <input type="number" id="x2" required>
  <input type="number" id="x3" required>
  <input type="number" id="x4" required>
  <input type="number" id="x5" required>

  <h3>Enter 5 values for Y:</h3>
  <input type="number" id="y1" required>
  <input type="number" id="y2" required>
  <input type="number" id="y3" required>
  <input type="number" id="y4" required>
  <input type="number" id="y5" required>

  <br><br>
  <button type="submit">Calculate</button>
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

  // Calculate averages
  const avgX = x.reduce((sum, val) => sum + val, 0) / x.length;
  const avgY = y.reduce((sum, val) => sum + val, 0) / y.length;

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

  // Display result
  document.getElementById('result').innerHTML =
    "<b>Average of X:</b> " + avgX.toFixed(2) + "<br>" +
    "<b>Average of Y:</b> " + avgY.toFixed(2) + "<br>" +
    "<b>Pearson Correlation (r):</b> " + r.toFixed(4);
});
</script>
