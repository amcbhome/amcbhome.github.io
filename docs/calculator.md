---
layout: page
title: "X and Y Average Calculator"
---

# X and Y Average Calculator

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
  <button type="submit">Calculate Averages</button>
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

  // Display result
  document.getElementById('result').textContent =
    "Average of X: " + avgX.toFixed(2) + " | Average of Y: " + avgY.toFixed(2);
});
</script>
