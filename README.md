# NazVid.github.io
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>NazVid</title>
<style>
  body, html {
    margin: 0; padding: 0; height: 100%;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background-color: black;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    position: relative;
  }
  #NazVidTimer {
    color: white;
    font-size: 5rem;
    font-weight: bold;
    user-select: none;
    position: relative;
    z-index: 1; /* Ensure timer is above overlay */
  }
  #overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.7); /* Semi-transparent black */
    display: flex;
    justify-content: up;
    align-items: up;
    color: white;
    font-size: 2rem;
    z-index: 0; /* Ensure overlay is below timer */
  }
</style>
</head>
<body>
<div id="overlay">Please wait until the timer finishes...</div>
<div id="NazVidTimer" aria-live="polite" aria-atomic="true">30:00</div>

<script>
  const timerDisplay = document.getElementById('NazVidTimer');
  const overlay = document.getElementById('overlay');
  let timeRemaining = 30 * 60; // 30 minutes in seconds

  function updateTimer() {
    let minutes = Math.floor(timeRemaining / 60);
    let seconds = timeRemaining % 60;
    timerDisplay.textContent =
      (minutes < 10 ? '0' : '') + minutes + ':' +
      (seconds < 10 ? '0' : '') + seconds;
  }

  function startCountdown() {
    updateTimer();
    const timerInterval = setInterval(() => {
      timeRemaining--;
      if (timeRemaining < 0) {
        clearInterval(timerInterval);
        timerDisplay.textContent = '00:00';
        overlay.style.display = 'none'; // Hide overlay when timer ends
      } else {
        updateTimer();
      }
    }, 1000);
  }

  // Start countdown immediately on page load
  startCountdown();
</script>
</body>
</html>
