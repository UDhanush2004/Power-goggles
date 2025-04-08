# Power-goggles
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Biomedical Parameters Dashboard</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      background: #0e0e0e;
      color: #fff;
      font-family: 'Segoe UI', sans-serif;
      margin: 0;
      padding: 20px;
    }
    h1 {
      text-align: center;
      margin-bottom: 30px;
      color: #00ffcc;
    }
    .grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 20px;
    }
    .card {
      background: #1e1e1e;
      padding: 20px;
      border-radius: 12px;
      box-shadow: 0 0 10px #00ffcc33;
    }
    .card h2 {
      color: #00ffcc;
      font-size: 1.2rem;
      margin-bottom: 10px;
    }
    #ecgCanvas {
      width: 100%;
      height: 150px;
      background: #111;
      border: 1px solid #555;
    }
  </style>
</head>
<body>

  <h1>Biomedical Parameters Dashboard</h1>

  <div class="grid">
    <div class="card"><h2>Heart Rate</h2><div id="heartRate">-- bpm</div></div>
    <div class="card"><h2>Pulse Rate</h2><div id="pulseRate">-- bpm</div></div>
    <div class="card"><h2>Sleep Cycle</h2><div id="sleepPhase">--</div></div>
    <div class="card"><h2>Stress Level</h2><div id="stressLevel">-- / 10</div></div>
    <div class="card"><h2>Cough Rate</h2><div id="coughCount">-- events</div></div>
    <div class="card"><h2>SpO₂ Level</h2><div id="spo2">-- %</div></div>
    <div class="card"><h2>Cardiac Cycle</h2><div id="cardiacPhase">--</div></div>
    <div class="card">
      <h2>ECG Waveform</h2>
      <canvas id="ecgCanvas" width="600" height="150"></canvas>
    </div>
  </div>

  <script>
    // Heart Rate
    function updateHeartRate() {
      document.getElementById("heartRate").textContent = `${Math.floor(Math.random() * 40 + 60)} bpm`;
    }
    // Pulse Rate
    function updatePulseRate() {
      document.getElementById("pulseRate").textContent = `${Math.floor(Math.random() * 30 + 65)} bpm`;
    }

    // Sleep Phase
    const sleepPhases = ["Awake", "Light Sleep", "Deep Sleep", "REM"];
    let sleepIndex = 0;
    function updateSleepPhase() {
      document.getElementById("sleepPhase").textContent = sleepPhases[sleepIndex];
      sleepIndex = (sleepIndex + 1) % sleepPhases.length;
    }

    // Stress Level
    function updateStressLevel() {
      document.getElementById("stressLevel").textContent = `${Math.floor(Math.random() * 11)} / 10`;
    }

    // Cough Rate
    let coughCount = 0;
    function updateCoughCount() {
      if (Math.random() < 0.3) coughCount++;
      document.getElementById("coughCount").textContent = `${coughCount} events`;
    }

    // SpO2
    function updateSpO2() {
      document.getElementById("spo2").textContent = `${Math.floor(Math.random() * 4 + 95)} %`;
    }

    // Cardiac Cycle
    const cardiacPhases = ["Diastole", "Atrial Systole", "Ventricular Systole"];
    let cardiacIndex = 0;
    function updateCardiacPhase() {
      document.getElementById("cardiacPhase").textContent = cardiacPhases[cardiacIndex];
      cardiacIndex = (cardiacIndex + 1) % cardiacPhases.length;
    }

    // ECG Waveform
    const canvas = document.getElementById("ecgCanvas");
    const ctx = canvas.getContext("2d");
    let t = 0;
    function drawECG() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      ctx.beginPath();
      ctx.moveTo(0, canvas.height / 2);
      for (let x = 0; x <= canvas.width; x++) {
        const y = canvas.height / 2 + Math.sin((x + t) * 0.05) * 30;
        ctx.lineTo(x, y);
      }
      ctx.strokeStyle = "#00ff99";
      ctx.lineWidth = 2;
      ctx.stroke();
      t += 2;
    }

    // Call All Updates
    setInterval(updateHeartRate, 2000);
    setInterval(updatePulseRate, 3000);
    setInterval(updateSleepPhase, 5000);
    setInterval(updateStressLevel, 4000);
    setInterval(updateCoughCount, 4000);
    setInterval(updateSpO2, 3000);
    setInterval(updateCardiacPhase, 4000);
    setInterval(drawECG, 100);

    // Initial call
    updateHeartRate();
    updatePulseRate();
    updateSleepPhase();
    updateStressLevel();
    updateCoughCount();
    updateSpO2();
    updateCardiacPhase();
    drawECG();
  </script>

</body>
</html>
