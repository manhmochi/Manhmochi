<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <title>Love Diary 🐾</title>
  <style>
    body {
      font-family: 'Comic Sans MS', cursive;
      background: url('https://i.imgur.com/YGxuBlJ.jpg') no-repeat center center fixed;
      background-size: cover;
      margin: 0;
      padding: 0;
      color: #333;
    }
    .container {
      max-width: 500px;
      margin: 80px auto;
      background: rgba(255, 255, 255, 0.9);
      padding: 30px;
      border-radius: 20px;
      box-shadow: 0 0 25px #ffaad4;
    }
    h1 {
      text-align: center;
      color: #ff69b4;
    }
    input, textarea, button {
      width: 100%;
      padding: 12px;
      margin: 10px 0;
      border: 2px solid #ffc0cb;
      border-radius: 10px;
      font-size: 16px;
    }
    button {
      background-color: #ff69b4;
      color: white;
      font-weight: bold;
      cursor: pointer;
    }
    .hidden {
      display: none;
    }
    .emoji {
      cursor: pointer;
      font-size: 24px;
      margin: 3px;
    }
    .note {
      background: #ffe6f0;
      padding: 12px;
      border-radius: 12px;
      margin-top: 10px;
      white-space: pre-wrap;
    }
    .timeline {
      margin-top: 20px;
    }
    .quote {
      text-align: center;
      font-style: italic;
      color: #d63384;
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <div class="container" id="auth">
    <h1>💕 Nhật Ký Tình Yêu 💕</h1>
    <input type="text" id="username" placeholder="Tên người yêu 💖">
    <input type="password" id="password" placeholder="Mật khẩu bí mật 🔒">
    <button onclick="register()">Đăng ký</button>
    <button onclick="login()">Đăng nhập</button>
  </div>

  <div class="container hidden" id="diary">
    <h1>📝 Viết Nhật Ký</h1>
    <div>
      <div>
        <span class="emoji" onclick="addEmoji('❤️')">❤️</span>
        <span class="emoji" onclick="addEmoji('🐱')">🐱</span>
        <span class="emoji" onclick="addEmoji('🌸')">🌸</span>
        <span class="emoji" onclick="addEmoji('💋')">💋</span>
        <span class="emoji" onclick="addEmoji('💌')">💌</span>
      </div>
      <textarea id="entry" rows="5" placeholder="Ghi điều gì đó ngọt ngào..."></textarea>
      <button onclick="saveEntry()">Lưu nhật ký</button>
    </div>
    <div class="timeline" id="entries"></div>
    <div class="quote">"Yêu là khi tim bạn cười mỗi lần nghĩ đến ai đó." 🐾</div>
    <button onclick="logout()">Đăng xuất</button>
  </div>

  <script>
    // Lưu trữ đơn giản bằng localStorage
    const users = JSON.parse(localStorage.getItem('users') || '{}');
    const entries = JSON.parse(localStorage.getItem('entries') || '{}');
    let currentUser = null;

    function register() {
      const user = document.getElementById('username').value.trim();
      const pass = document.getElementById('password').value;
      if (!user || !pass) return alert('Điền đầy đủ thông tin nhé!');
      if (users[user]) return alert('Tên này đã có rồi 🥺');
      users[user] = pass;
      localStorage.setItem('users', JSON.stringify(users));
      alert('Đăng ký thành công 💕');
    }

    function login() {
      const user = document.getElementById('username').value.trim();
      const pass = document.getElementById('password').value;
      if (users[user] === pass) {
        currentUser = user;
        showDiary();
      } else {
        alert('Sai tên hoặc mật khẩu 😿');
      }
    }

    function logout() {
      currentUser = null;
      document.getElementById('diary').classList.add('hidden');
      document.getElementById('auth').classList.remove('hidden');
    }

    function showDiary() {
      document.getElementById('auth').classList.add('hidden');
      document.getElementById('diary').classList.remove('hidden');
      loadEntries();
    }

    function addEmoji(emoji) {
      document.getElementById('entry').value += emoji;
    }

    function saveEntry() {
      const text = document.getElementById('entry').value.trim();
      if (!text) return;
      if (!entries[currentUser]) entries[currentUser] = [];
      entries[currentUser].push({ text, time: new Date().toLocaleString() });
      localStorage.setItem('entries', JSON.stringify(entries));
      document.getElementById('entry').value = '';
      loadEntries();
    }

    function loadEntries() {
      const list = document.getElementById('entries');
      list.innerHTML = '';
      (entries[currentUser] || []).slice().reverse().forEach(e => {
        const div = document.createElement('div');
        div.className = 'note';
        div.innerHTML = `<strong>${e.time}</strong><br>${e.text}`;
        list.appendChild(div);
      });
    }
  </script>
</body>
</html>