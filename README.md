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
      transition: all 0.3s ease;
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
    select:focus {
      outline: none;
      border-color: #00ddeb;
      box-shadow: 0 0 12px rgba(0, 221, 235, 0.7);
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
      border-radius: 10px;
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
      text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.3);
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

  <script>
    // Khởi tạo mảng lưu trữ đăng ký và danh sách người dùng
    const registrations = {};
    const users = new Set();

    // Tạo các tùy chọn số từ 1 đến 150
    const numberSelect = document.getElementById('number');
    for (let i = 1; i <= 150; i++) {
      const option = document.createElement('option');
      option.value = i;
      option.textContent = i;
      numberSelect.appendChild(option);
    }

    // Hàm đăng ký
    function register() {
      const username = document.getElementById('username').value.trim();
      const number = document.getElementById('number').value;
      const error = document.getElementById('error');

      // Kiểm tra đầu vào
      if (!username || !number) {
        error.textContent = 'Vui lòng nhập tên và chọn số!';
        return;
      }

      // Kiểm tra người dùng đã đăng ký số khác chưa
      if (users.has(username)) {
        error.textContent = `Bạn đã đăng ký một số khác! Mỗi người chỉ được chọn một số.`;
        return;
      }

      // Kiểm tra số đã được đăng ký chưa
      if (registrations[number]) {
        error.textContent = `Số ${number} đã được đăng ký bởi ${registrations[number]}!`;
        return;
      }

      // Lưu đăng ký
      registrations[number] = username;
      users.add(username);
      error.textContent = '';
      localStorage.setItem('registrations', JSON.stringify(registrations)); // Lưu vào localStorage

      // Cập nhật danh sách và trạng thái số
      updateRegisteredList();
      updateNumberOptions();

      // Reset form
      document.getElementById('username').value = '';
      document.getElementById('number').value = '';
    }

    // Hàm cập nhật danh sách đã đăng ký
    function updateRegisteredList() {
      const registeredList = document.getElementById('registeredList');
      registeredList.innerHTML = '';
      for (const [number, username] of Object.entries(registrations).sort((a, b) => a[0] - b[0])) {
        const li = document.createElement('li');
        li.textContent = `Số ${number}: ${username}`;
        registeredList.appendChild(li);
      }
    }

    // Hàm cập nhật trạng thái các số trong menu thả xuống
    function updateNumberOptions() {
      const options = numberSelect.getElementsByTagName('option');
      for (let i = 1; i < options.length; i++) {
        const number = options[i].value;
        if (registrations[number]) {
          options[i].disabled = true;
          options[i].style.color = 'red';
        } else {
          options[i].disabled = false;
          options[i].style.color = '';
        }
      }
    }

    // Khôi phục dữ liệu từ localStorage khi tải trang
    window.onload = function() {
      const savedRegistrations = JSON.parse(localStorage.getItem('registrations')) || {};
      Object.assign(registrations, savedRegistrations);
      for (const username of Object.values(registrations)) {
        users.add(username);
      }
      updateRegisteredList();
      updateNumberOptions();
    };
  </script>
</body>
</html>
