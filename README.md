<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Happy Valentine's Day</title>
  <style>
    @font-face {
      font-family: 'Edwardian Script ITC';
      src: url('EdwardianScriptITC.ttf') format('truetype');
    }

    body {
      margin: 0;
      padding: 0;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background-color: #ffebee;
      font-family: 'Arial', sans-serif;
      overflow: hidden;
    }

    .envelope-container {
      position: relative;
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    .envelope {
      position: relative;
      width: 300px;
      height: 200px;
      background-color: #d32f2f;
      border-radius: 10px;
      display: flex;
      justify-content: center;
      align-items: center;
      cursor: pointer;
      box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
      transition: transform 1s ease-in-out;
    }

    .flap {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 50%;
      background-color: #b71c1c;
      border-radius: 10px 10px 0 0;
      transform-origin: top;
      transition: transform 1s ease-in-out;
    }

    .message {
      position: absolute;
      width: 90%;
      height: 70%;
      background: white;
      color: #d32f2f;
      font-size: 24px;
      font-weight: bold;
      display: flex;
      justify-content: center;
      align-items: center;
      border-radius: 5px;
      box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
      opacity: 0;
      transition: opacity 1s ease-in-out 0.5s;
    }

    .open-text {
      margin-top: 15px;
      font-size: 26px;
      font-weight: bold;
      color: #d32f2f;
      text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
      transition: opacity 0.5s ease-in-out;
    }

    .text {
      position: absolute;
      font-size: 60px;
      color: #d32f2f;
      text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
      z-index: 2;
      opacity: 0;
      transition: opacity 1s ease-in-out 1s;
      font-family: 'Edwardian Script ITC', cursive;
    }

    .heart, .rose {
      position: absolute;
      animation: float 6s infinite ease-in-out;
      z-index: 1;
    }

    .heart {
      width: 50px;
      height: 45px;
    }

    .heart:before,
    .heart:after {
      position: absolute;
      content: "";
      left: 25px;
      top: 0;
      width: 25px;
      height: 40px;
      background: red;
      border-radius: 25px 25px 0 0;
      transform: rotate(-45deg);
      transform-origin: 0 100%;
    }

    .heart:after {
      left: 0;
      transform: rotate(45deg);
      transform-origin: 100% 100%;
    }

    .rose {
      width: 50px;
      height: 50px;
      background-image: url('https://www.transparentpng.com/thumb/rose/red-rose-png-0.png');
      background-size: cover;
    }

    @keyframes float {
      0%, 100% {
        transform: translateY(0);
      }
      50% {
        transform: translateY(-20px);
      }
    }
  </style>
</head>
<body>
  <div class="envelope-container">
    <div class="envelope" onclick="openEnvelope()">
      <div class="flap"></div>
      <div class="message">Click to Open</div>
    </div>
    <div class="open-text">Open Me</div>
  </div>
  
  <div class="text">Happy Valentine's Day ❤️</div>

  <script>
    const container = document.body;

    function createElement(type) {
      const element = document.createElement('div');
      element.classList.add(type);
      container.appendChild(element);
      return element;
    }

    function moveElement(element) {
      let x, y;

      do {
        x = Math.random() * (window.innerWidth - 50);
        y = Math.random() * (window.innerHeight - 50);
      } while (x > window.innerWidth / 2 - 200 && x < window.innerWidth / 2 + 200 &&
               y > window.innerHeight / 2 - 100 && y < window.innerHeight / 2 + 100);

      element.style.left = `${x}px`;
      element.style.top = `${y}px`;
    }

    function openEnvelope() {
      const flap = document.querySelector('.flap');
      const message = document.querySelector('.message');
      const text = document.querySelector('.text');
      const envelope = document.querySelector('.envelope');
      const openText = document.querySelector('.open-text');

      // Fade out "Open Me" text
      openText.style.opacity = "0";

      // Open the envelope animation
      flap.style.transform = "rotateX(180deg)";
      message.style.opacity = "0";

      // Fade in main content after opening
      setTimeout(() => {
        text.style.opacity = "1";
        envelope.style.transform = "scale(0)"; // Hide envelope after opening

        for (let i = 0; i < 50; i++) {
          const heart = createElement('heart');
          const rose = createElement('rose');
          moveElement(heart);
          moveElement(rose);
        }

        setInterval(() => {
          document.querySelectorAll('.heart, .rose').forEach(element => {
            moveElement(element);
          });
        }, 2000);
      }, 1000);
    }
  </script>
</body>
</html>
