<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>I'm Sorry 🥺</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }
    body {
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      /* Soft pink pastel gradient background */
      background: linear-gradient(135deg, #ffc0cb 0%, #ffb6c1 50%, #ff69b4 100%);
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }
    .card {
      background: rgba(255, 255, 255, 0.95);
      padding: 40px 30px;
      border-radius: 20px;
      box-shadow: 0 10px 30px rgba(255, 105, 180, 0.3);
      text-align: center;
      max-width: 400px;
      width: 90%;
      position: relative;
      min-height: 280px;
    }
    h1 {
      color: #d63384;
      font-size: 26px;
      margin-bottom: 12px;
    }
    p {
      color: #555;
      font-size: 16px;
      margin-bottom: 30px;
    }
    .btn-group {
      display: flex;
      justify-content: center;
      gap: 15px;
      position: relative;
      min-height: 50px;
    }
    button {
      padding: 12px 28px;
      font-size: 16px;
      font-weight: bold;
      border: none;
      border-radius: 25px;
      cursor: pointer;
      transition: transform 0.2s ease, opacity 0.3s ease;
    }
    #yesBtn {
      background-color: #28a745;
      color: white;
      box-shadow: 0 4px 12px rgba(40, 167, 69, 0.3);
    }
    #yesBtn:hover {
      transform: scale(1.1);
    }
    #noBtn {
      background-color: #dc3545;
      color: white;
      position: absolute;
      box-shadow: 0 4px 12px rgba(220, 53, 69, 0.3);
    }
    .success-msg {
      display: none;
      font-size: 22px;
      color: #d63384;
      font-weight: bold;
    }
  </style>
</head>
<body>

  <div class="card" id="apologyCard">
    <div id="interactiveContent">
      <h1>I'm so sorry! 🥺</h1>
      <p>Will you forgive me?</p>
      
      <div class="btn-group" id="btnGroup">
        <button id="yesBtn" onclick="acceptApology()">Yes</button>
        <button id="noBtn">No</button>
      </div>
    </div>

    <div id="successMsg" class="success-msg">
      Yay! ❤️ Thank you for forgiving me! 🥰
    </div>
  </div>

  <script>
    const noBtn = document.getElementById('noBtn');
    const btnGroup = document.getElementById('btnGroup');
    let attempts = 0;
    const maxAttempts = 5;

    // Set initial layout position for No button
    noBtn.style.right = '40px';

    function moveButton() {
      attempts++;
      
      if (attempts >= maxAttempts) {
        noBtn.style.opacity = '0';
        setTimeout(() => {
          noBtn.style.display = 'none';
        }, 300);
        return;
      }

      // Calculate safe bounds within the container
      const containerRect = btnGroup.getBoundingClientRect();
      const btnRect = noBtn.getBoundingClientRect();

      const maxX = containerRect.width - btnRect.width;
      const maxY = containerRect.height - btnRect.height;

      const randomX = Math.max(0, Math.floor(Math.random() * maxX));
      const randomY = Math.max(-50, Math.floor(Math.random() * 100)); // allow floating movement

      noBtn.style.left = `${randomX}px`;
      noBtn.style.top = `${randomY}px`;
      noBtn.style.right = 'auto';
    }

    // Move on mouse enter (desktop) and touch start (mobile)
    noBtn.addEventListener('mouseenter', moveButton);
    noBtn.addEventListener('touchstart', (e) => {
      e.preventDefault();
      moveButton();
    });

    function acceptApology() {
      document.getElementById('interactiveContent').style.display = 'none';
      document.getElementById('successMsg').style.display = 'block';
    }
  </script>
</body>
</html>
