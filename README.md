<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Give Away Khóa Cô Mai Phương</title>
  <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700&family=Dancing+Script:wght@700&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Orbitron', sans-serif;
      max-width: 800px;
      margin: 0 auto;
      padding: 20px;
      background: linear-gradient(135deg, #1a0d2b, #3c1b5e);
      color: #fff;
      min-height: 100vh;
    }
    h1 {
      text-align: center;
      font-family: 'Dancing Script', cursive;
      color: #ff6f61;
      text-shadow: 3px 3px 6px rgba(0, 0, 0, 0.4);
      font-size: 3em;
      margin-bottom: 30px;
      letter-spacing: 2px;
      line-height: 1.2;
    }
    .form-container {
      background: rgba(255, 255, 255, 0.05);
      backdrop-filter: blur(12px);
      padding: 30px;
      border-radius: 20px;
      box-shadow: 0 0 20px rgba(255, 105, 97, 0.3);
      border: 2px solid transparent;
      border-image: linear-gradient(45deg, #ff6f61, #00ddeb) 1;
      margin-bottom: 30px;
      display: flex;
      flex-direction: column;
      align-items: center;
      max-width: 400px;
      margin-left: auto;
      margin-right: auto;
    }
    .form-container:hover {
      transform: translateY(-5px);
      box-shadow: 0 0 30px rgba(255, 105, 97, 0.5);
    }
    input, select, button {
      margin: 10px 0;
      padding: 12px;
      width: 90%;
      box-sizing: border-box;
      border-radius: 10px;
      font-family: 'Orbitron', sans-serif;
      font-size: 1em;
      transition: all 0.3s ease;
    }
    input {
      background: rgba(255, 255, 255, 0.1);
      border: 2px solid #ff6f61;
      color: #fff;
    }
    input:focus {
      outline: none;
      border-color: #00ddeb;
      box-shadow: 0 0 12px rgba(0, 221, 235, 0.7);
    }
    select {
      background: rgba(255, 255, 255, 0.1);
      border: 2px solid #ff6f61;
      color: #fff;
    }
    select option {
      background: #2c3e50;
      color: #fff;
    }
    select option[disabled] {
      color: red;
      font-weight: bold;
    }
    button {
      background: linear-gradient(45deg, #ff6f61, #ffb88c);
      color: white;
      border: none;
      cursor: pointer;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 1px;
    }
    button:hover {
      background: linear-gradient(45deg, #e65b50, #ff9f68);
      transform: scale(1.05);
      box-shadow: 0 0 15px rgba(255, 105, 97, 0.7);
    }
    .registered-list {
      background: rgba(255, 255, 255, 0.05);
      backdrop-filter: blur(12px);
      padding: 30px;
      border-radius: 20px;
      box-shadow: 0 0 20px rgba(255, 105, 97, 0.3);
      border: 2px solid transparent;
      border-image: linear-gradient(45deg, #ff6f61, #00ddeb) 1;
      transition: all 0.3s ease;
    }
    .registered-list:hover {
      transform: translateY(-5px);
      box-shadow: 0 0 30px rgba(255, 105, 97, 0.5);
    }
    .registered-list ul {
      list-style: none;
      padding: 0;
    }
    .registered-list li {
      padding: 10px 0;
      border-bottom: 1px solid rgba(255, 255, 255, 0.2);
      color: #fff;
      font-size: 1.1em;
    }
    .error {
      color: #ff4444;
      font-size: 1em;
      text-align: center;
    }
  </style>
</head>
<body>
  <h1>Give Away Khóa Cô Mai Phương</h1>
  <div class="form-container">
    <input type="text" id="username" placeholder="Nhập tên của bạn" required>
    <select id="number">
      <option value="">Chọn số (1-150)</option>
    </select>
    <button onclick="register()">Đăng ký</button>
    <p id="error" class="error"></p>
  </div>
  <div class="registered-list">
    <h2>Danh sách đã đăng ký</h2>
    <ul id="registeredList"></ul>
  </div>

  <!-- Firebase SDK & App Logic -->
  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/11.8.1/firebase-app.js";
    import { getDatabase, ref, onValue, set, get } from "https://www.gstatic.com/firebasejs/11.8.1/firebase-database.js";

    const firebaseConfig = {
      apiKey: "AIzaSyCyn-1cKitPlfJ9Kx4JMB0p0qsDRqzi4Ow",
      authDomain: "test-5a33b.firebaseapp.com",
      databaseURL: "https://test-5a33b-default-rtdb.firebaseio.com",
      projectId: "test-5a33b",
      storageBucket: "test-5a33b.firebasestorage.app",
      messagingSenderId: "571352379860",
      appId: "1:571352379860:web:b295e893cd572ff9fba641",
      measurementId: "G-DGFZ3TZ90M"
    };

    const app = initializeApp(firebaseConfig);
    const db = getDatabase(app);
    const registrationsRef = ref(db, 'registrations');

    const numberSelect = document.getElementById('number');
    for (let i = 1; i <= 150; i++) {
      const option = document.createElement('option');
      option.value = i;
      option.textContent = i;
      numberSelect.appendChild(option);
    }

    onValue(registrationsRef, (snapshot) => {
      const data = snapshot.val() || {};
      updateRegisteredList(data);
      updateNumberOptions(data);
    });

    window.register = async function() {
      const usernameInput = document.getElementById('username');
      const numberInput = document.getElementById('number');
      const error = document.getElementById('error');
      const username = usernameInput.value.trim();
      const number = numberInput.value;

      if (!username || !number) {
        error.textContent = "Vui lòng nhập tên và chọn số!";
        return;
      }

      const snapshot = await get(registrationsRef);
      const data = snapshot.val() || {};

      if (Object.values(data).includes(username)) {
        error.textContent = "Bạn đã đăng ký một số khác!";
        return;
      }

      if (data[number]) {
        error.textContent = `Số ${number} đã được đăng ký bởi ${data[number]}!`;
        return;
      }

      await set(ref(db, `registrations/${number}`), username);
      error.style.color = "#00ff99";
      error.textContent = `✅ Đăng ký thành công số ${number} cho ${username}!`;
      usernameInput.value = '';
      numberInput.value = '';
    };

    function updateRegisteredList(data) {
      const list = document.getElementById('registeredList');
      list.innerHTML = '';
      Object.entries(data)
        .sort((a, b) => a[0] - b[0])
        .forEach(([number, name]) => {
          const li = document.createElement('li');
          li.textContent = `Số ${number}: ${name}`;
          list.appendChild(li);
        });
    }

    function updateNumberOptions(data) {
      const options = numberSelect.getElementsByTagName('option');
      for (let i = 1; i < options.length; i++) {
        const number = options[i].value;
        if (data[number]) {
          options[i].disabled = true;
          options[i].textContent = `${number} (Đã chọn)`;
          options[i].style.color = 'red';
        } else {
          options[i].disabled = false;
          options[i].textContent = number;
          options[i].style.color = '';
        }
      }
    }
  </script>
</body>
</html>
