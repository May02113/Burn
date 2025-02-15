<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <title>Письмо в огне</title>
  <style>
    body {
      margin: 0;
      background: #111;
      color: #fff;
      font-family: sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
    .container {
      text-align: center;
      background: #222;
      padding: 20px;
      border-radius: 10px;
      position: relative;
      overflow: hidden;
      width: 90%;
      max-width: 600px;
    }
    textarea {
      width: 100%;
      height: 200px;
      padding: 10px;
      border: none;
      border-radius: 5px;
      font-size: 16px;
      resize: none;
      background: #333;
      color: #fff;
    }
    button {
      margin-top: 15px;
      padding: 10px 20px;
      background: #e74c3c;
      color: #fff;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      font-size: 16px;
    }
    .burn {
      animation: burn 3s forwards;
      position: relative;
      z-index: 2;
    }
    .smoke {
      content: "";
      position: absolute;
      top: 0;
      left: 50%;
      width: 50px;
      height: 50px;
      background: radial-gradient(circle, rgba(200,200,200,0.8) 0%, rgba(200,200,200,0) 70%);
      border-radius: 50%;
      opacity: 0;
      transform: translate(-50%, 0) scale(0.5);
      pointer-events: none;
      animation: smoke 3s forwards;
      z-index: 1;
    }
    @keyframes burn {
      0% {
        filter: brightness(1) contrast(1);
        transform: rotate(0deg) scale(1);
        opacity: 1;
      }
      25% {
        filter: brightness(1.2) contrast(1.1);
        transform: rotate(2deg) scale(0.98);
        opacity: 0.8;
      }
      50% {
        filter: brightness(1.5) contrast(1.2);
        transform: rotate(-2deg) scale(0.95);
        opacity: 0.6;
      }
      75% {
        filter: brightness(0.8) contrast(0.9);
        transform: rotate(5deg) scale(0.9);
        opacity: 0.4;
      }
      100% {
        filter: brightness(0.5) contrast(0.8);
        transform: rotate(10deg) scale(0.8);
        opacity: 0;
      }
    }
    @keyframes smoke {
      0% {
        opacity: 0;
        transform: translate(-50%, 0) scale(0.5);
      }
      50% {
        opacity: 0.6;
        transform: translate(-50%, -30px) scale(1);
      }
      100% {
        opacity: 0;
        transform: translate(-50%, -60px) scale(1.5);
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Письмо в огне</h1>
    <textarea id="letter" placeholder="Напишите ваше письмо здесь..."></textarea>
    <br>
    <button onclick="burnLetter()">Сжечь письмо</button>
    <p id="message"></p>
  </div>
  <script>
    function burnLetter() {
      var letter = document.getElementById('letter');
      var message = document.getElementById('message');
      if (letter.value.trim() === "") {
        alert("Пожалуйста, напишите письмо перед сжиганием!");
        return;
      }
      // Создаем элемент дыма
      var smoke = document.createElement('div');
      smoke.classList.add('smoke');
      letter.parentElement.appendChild(smoke);

      // Запускаем анимацию горения
      letter.classList.add('burn');

      // По окончании анимации очищаем текст и удаляем дым
      setTimeout(function(){
        letter.value = "";
        letter.classList.remove('burn');
        if (smoke.parentElement) {
          smoke.parentElement.removeChild(smoke);
        }
        message.innerText = "Ваше письмо было виртуально сожжено.";
      }, 3000);
    }
  </script>
</body>
</html>
