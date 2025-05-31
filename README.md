<!DOCTYPE html><html lang="vi">
<head>
  <meta charset="UTF-8">
  <title>Góc Tình Yêu 💖</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: #ffe6f0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }
    .login-box, .editor-box {
      background: white;
      padding: 20px;
      border-radius: 16px;
      box-shadow: 0 0 15px rgba(0,0,0,0.1);
      width: 350px;
      display: none;
    }
    .login-box.active, .editor-box.active {
      display: block;
    }
    h2 {
      color: #d63384;
      text-align: center;
    }
    input[type="text"], input[type="password"], textarea {
      width: 100%;
      padding: 10px;
      margin-top: 10px;
      border: 1px solid #ccc;
      border-radius: 8px;
      font-size: 14px;
    }
    button {
      background: #ff66a3;
      color: white;
      padding: 10px 20px;
      margin-top: 15px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      width: 100%;
    }
    .emoji-box span {
      cursor: pointer;
      font-size: 18px;
      margin: 5px;
    }
  </style>
</head>
<body>
  <div class="login-box active" id="loginBox">
    <h2>Đăng nhập 💌</h2>
    <input type="text" id="username" placeholder="Tên người dùng">
    <input type="password" id="password" placeholder="Mật khẩu">
    <button onclick="login()">Vào góc tình yêu</button>
  </div>  <div class="editor-box" id="editorBox">
    <h2>Góc viết yêu thương ✨</h2>
    <textarea id="textArea" rows="10" placeholder="Viết điều bạn muốn..."></textarea>
    <div class="emoji-box">
      <span onclick="addEmoji('🥰')">🥰</span>
      <span onclick="addEmoji('😍')">😍</span>
      <span onclick="addEmoji('😭')">😭</span>
      <span onclick="addEmoji('💕')">💕</span>
      <span onclick="addEmoji('🌹')">🌹</span>
    </div>
    <button onclick="saveText()">Lưu lại</button>
  </div>  <script>
    const loginBox = document.getElementById('loginBox');
    const editorBox = document.getElementById('editorBox');

    function login() {
      const user = document.getElementById('username').value;
      const pass = document.getElementById('password').value;

      if (user && pass) {
        loginBox.classList.remove('active');
        editorBox.classList.add('active');
      } else {
        alert("Vui lòng nhập đầy đủ tên và mật khẩu.");
      }
    }

    function addEmoji(emoji) {
      const textArea = document.getElementById('textArea');
      textArea.value += emoji;
    }

    function saveText() {
      const content = document.getElementById('textArea').value;
      localStorage.setItem('loveNote', content);
      alert("Đã lưu lại trong tim 💗 (localStorage)");
    }

    // Tải lại nội dung nếu có
    window.onload = () => {
      const saved = localStorage.getItem('loveNote');
      if (saved) document.getElementById('textArea').value = saved;
    }
  </script></body>
</html>