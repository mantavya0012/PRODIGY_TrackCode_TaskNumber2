# PRODIGY_TrackCode_TaskNumber2
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Stopwatch</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background: linear-gradient(135deg, #6a85b6, #bac8e0);
    }

    .stopwatch-container {
      background: rgba(255, 255, 255, 0.1);
      backdrop-filter: blur(10px);
      padding: 30px;
      border-radius: 20px;
      text-align: center;
      width: 320px;
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
    }

    .time-display {
      font-size: 3rem;
      color: #fff;
      margin-bottom: 20px;
    }

    .buttons {
      display: flex;
      justify-content: center;
      gap: 10px;
      margin-bottom: 20px;
    }

    .buttons button {
      background: #fff;
      border: none;
      padding: 10px 20px;
      border-radius: 8px;
      cursor: pointer;
      font-weight: bold;
      transition: transform 0.2s ease, background 0.3s ease;
    }

    .buttons button:hover {
      background: #f0f0f0;
      transform: translateY(-2px);
    }

    .laps {
      max-height: 150px;
      overflow-y: auto;
    }

    .laps div {
      background: rgba(255, 255, 255, 0.2);
      color: #fff;
      padding: 8px;
      margin: 5px 0;
      border-radius: 8px;
      font-size: 1rem;
    }
  </style>
</head>
<body>
  <div class="stopwatch-container">
    <div class="time-display" id="time">00:00:00</div>
    <div class="buttons">
      <button id="start">Start</button>
      <button id="pause">Pause</button>
      <button id="reset">Reset</button>
      <button id="lap">Lap</button>
    </div>
    <div class="laps" id="laps"></div>
  </div>

  <script>
    let startTime = 0;
    let elapsedTime = 0;
    let timerInterval;
    let running = false;

    const timeDisplay = document.getElementById('time');
    const lapsContainer = document.getElementById('laps');

    document.getElementById('start').addEventListener('click', () => {
      if (!running) {
        running = true;
        startTime = Date.now() - elapsedTime;
        timerInterval = setInterval(updateTime, 10);
      }
    });

    document.getElementById('pause').addEventListener('click', () => {
      if (running) {
        running = false;
        clearInterval(timerInterval);
      }
    });

    document.getElementById('reset').addEventListener('click', () => {
      running = false;
      clearInterval(timerInterval);
      elapsedTime = 0;
      updateTime();
      lapsContainer.innerHTML = '';
    });

    document.getElementById('lap').addEventListener('click', () => {
      if (running) {
        const lapTime = document.createElement('div');
        lapTime.textContent = `Lap: ${formatTime(elapsedTime)}`;
        lapsContainer.appendChild(lapTime);
      }
    });

    function updateTime() {
      elapsedTime = Date.now() - startTime;
      timeDisplay.textContent = formatTime(elapsedTime);
    }

    function formatTime(ms) {
      let totalSeconds = Math.floor(ms / 1000);
      let minutes = Math.floor(totalSeconds / 60);
      let seconds = totalSeconds % 60;
      let milliseconds = Math.floor((ms % 1000) / 10);

      return `${pad(minutes)}:${pad(seconds)}:${pad(milliseconds)}`;
    }

    function pad(num) {
      return num.toString().padStart(2, '0');
    }
  </script>
</body>
</html>

