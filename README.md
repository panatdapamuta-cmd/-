<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  
  <title>System Status - Processing</title>
  <meta property="og:title" content="Delivery Status: In Transit" />
  <meta property="og:description" content="Click to view full delivery tracking report." />

  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; -webkit-tap-highlight-color: transparent; }
    
    body {
      /* โทนสีน้ำตาลเบจ อบอุ่น มินิมอล */
      background: linear-gradient(180deg, #faf6f0 0%, #f3ece1 50%, #e8dec8 100%);
      height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      overflow: hidden;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", sans-serif;
    }

    .container {
      width: 100%;
      height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      position: relative;
    }

    /* ปุ่มเปิดรับของขวัญ - โทนน้ำตาลอบอุ่น */
    .start-btn {
      padding: 16px 42px;
      font-size: 19px;
      font-weight: bold;
      color: #ffffff;
      background: linear-gradient(135deg, #c49a6c 0%, #a07855 100%);
      border: none;
      border-radius: 50px;
      cursor: pointer;
      box-shadow: 0 10px 30px rgba(160, 120, 85, 0.35);
      z-index: 10;
      animation: pulse 1.8s infinite ease-in-out;
      letter-spacing: 0.5px;
    }

    @keyframes pulse {
      0%, 100% { transform: scale(1); }
      50% { transform: scale(1.05); }
    }

    /* ฉากหลังอนิเมชั่น */
    .stage {
      display: none;
      flex-direction: column;
      align-items: center;
      justify-content: space-between;
      height: 85vh;
      width: 100%;
      padding: 40px 20px;
      position: relative;
    }

    /* ตัวการ์ตูนหมาอ้วนหงอย */
    .character-wrap {
      position: relative;
      display: flex;
      flex-direction: column;
      align-items: center;
      margin-top: 60px;
      animation: sad-sway 3s infinite ease-in-out;
    }

    /* SVG น้องหมาตัวอ้วนสีน้ำตาล */
    .sad-dog {
      width: 210px;
      height: 210px;
      filter: drop-shadow(0 15px 25px rgba(120, 90, 60, 0.15));
    }

    /* เงาใต้น้องหมา */
    .shadow {
      width: 150px;
      height: 20px;
      background: rgba(140, 105, 75, 0.2);
      border-radius: 50%;
      margin-top: -12px;
      filter: blur(5px);
      animation: shadow-breath 3s infinite ease-in-out;
    }

    /* กล่องข้อความสไตล์การ์ดเบจมินิมอล */
    .speech-bubble {
      background: rgba(255, 253, 249, 0.92);
      backdrop-filter: blur(15px);
      border: 2px solid #ffffff;
      padding: 22px 38px;
      border-radius: 30px;
      box-shadow: 0 20px 40px rgba(140, 105, 75, 0.15);
      text-align: center;
      animation: pop-up 0.7s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards;
      margin-bottom: 35px;
    }

    .speech-bubble p {
      font-size: 22px;
      font-weight: 800;
      color: #6b4c35; /* สีน้ำตาลเข้มละมุน */
      letter-spacing: 0.5px;
    }

    /* หัวใจดวงเล็กลอยจางๆ */
    .floating-heart {
      position: absolute;
      color: #b8860b;
      font-size: 20px;
      pointer-events: none;
      animation: fall 3.5s linear infinite;
      opacity: 0.7;
    }

    @keyframes sad-sway {
      0%, 100% { transform: translateY(0) rotate(0deg); }
      50% { transform: translateY(-12px) rotate(-1.5deg); }
    }

    @keyframes shadow-breath {
      0%, 100% { transform: scale(1); opacity: 0.4; }
      50% { transform: scale(0.85); opacity: 0.2; }
    }

    @keyframes pop-up {
      0% { transform: scale(0.6); opacity: 0; }
      100% { transform: scale(1); opacity: 1; }
    }

    @keyframes fall {
      0% { transform: translateY(-20px) rotate(0deg); opacity: 0; }
      20% { opacity: 0.8; }
      100% { transform: translateY(80vh) rotate(180deg); opacity: 0; }
    }
  </style>
</head>
<body>

  <div class="container">
    <button class="start-btn" id="startBtn" onclick="openPresent()">📦 กดเปิดดูของขวัญ</button>

    <div class="stage" id="stage">
      <div class="character-wrap">
        
        <!-- SVG น้องหมาอ้วนหงอย โทนสีน้ำตาลเบจ -->
        <svg class="sad-dog" viewBox="0 0 200 200">
          <defs>
            <!-- ไล่สีขนสีเบจ/น้ำตาลอบอุ่น -->
            <linearGradient id="dogBody" x1="0%" y1="0%" x2="0%" y2="100%">
              <stop offset="0%" stop-color="#e8cca4" />
              <stop offset="100%" stop-color="#d1ab7b" />
            </linearGradient>
            <linearGradient id="dogEar" x1="0%" y1="0%" x2="0%" y2="100%">
              <stop offset="0%" stop-color="#a87c51" />
              <stop offset="100%" stop-color="#8c6239" />
            </linearGradient>
          </defs>

          <!-- หูตกข้างซ้าย -->
          <path d="M 45 65 C 20 70 10 110 25 130 C 35 140 50 120 52 95 Z" fill="url(#dogEar)"/>
          
          <!-- หูตกข้างขวา -->
          <path d="M 155 65 C 180 70 190 110 175 130 C 165 140 150 120 148 95 Z" fill="url(#dogEar)"/>

          <!-- ตัวหมาอ้วนกลม -->
          <ellipse cx="100" cy="145" rx="65" ry="48" fill="url(#dogBody)"/>
          
          <!-- พุงขาวนวล -->
          <ellipse cx="100" cy="152" rx="42" ry="32" fill="#fffaf2"/>

          <!-- หัวกลมโต -->
          <circle cx="100" cy="92" r="50" fill="url(#dogBody)"/>

          <!-- ขาหน้านั่งหงอย -->
          <ellipse cx="78" cy="172" rx="14" ry="18" fill="#d1ab7b"/>
          <ellipse cx="122" cy="172" rx="14" ry="18" fill="#d1ab7b"/>
          <circle cx="78" cy="184" r="11" fill="#fffaf2"/>
          <circle cx="122" cy="184" r="11" fill="#fffaf2"/>

          <!-- ตาเศร้า/ตาอ้อนหงอยๆ -->
          <ellipse cx="78" cy="88" rx="6" ry="9" fill="#3d2b1f"/>
          <ellipse cx="122" cy="88" rx="6" ry="9" fill="#3d2b1f"/>
          <!-- ไฮไลต์ตา -->
          <circle cx="80" cy="85" r="2.5" fill="#ffffff"/>
          <circle cx="124" cy="85" r="2.5" fill="#ffffff"/>

          <!-- คิ้วตก ตกแต่งความหงอย -->
          <path d="M 70 73 Q 78 77 86 75" stroke="#7a5535" stroke-width="3.5" stroke-linecap="round" fill="none"/>
          <path d="M 130 73 Q 122 77 114 75" stroke="#7a5535" stroke-width="3.5" stroke-linecap="round" fill="none"/>

          <!-- ปากนุ่มฟู + จมูกดำ -->
          <ellipse cx="100" cy="100" rx="18" ry="12" fill="#fffaf2"/>
          <ellipse cx="100" cy="96" rx="8" ry="5" fill="#3d2b1f"/>
          <!-- ปากคว่ำหงอยๆ -->
          <path d="M 93 106 Q 100 102 107 106" stroke="#523a28" stroke-width="2.5" stroke-linecap="round" fill="none"/>

          <!-- แก้มอมชมพูนิดๆ -->
          <circle cx="65" cy="100" r="7" fill="#e8a598" opacity="0.4"/>
          <circle cx="135" cy="100" r="7" fill="#e8a598" opacity="0.4"/>

          <!-- หยดน้ำตา/ความหงอยเล็กๆ -->
          <path d="M 128 97 C 128 101 125 104 125 104 C 125 104 122 101 122 97 C 122 95 125 93 125 93 C 125 93 128 95 128 97 Z" fill="#70b5f5" opacity="0.8"/>
        </svg>

        <div class="shadow"></div>
      </div>

      <div class="speech-bubble">
        <p>🥺 คิดถึงจะแย่แล้ว...</p>
      </div>
    </div>
  </div>

  <script>
    function openPresent() {
      document.getElementById('startBtn').style.display = 'none';
      document.getElementById('stage').style.display = 'flex';
      
      // เอฟเฟกต์ใบไม้/หัวใจสีเบจลอยเบาๆ
      setInterval(() => {
        const item = document.createElement('div');
        item.className = 'floating-heart';
        item.innerHTML = ['🤎', '✨', '🐾', '🌾', '🤍'][Math.floor(Math.random()*5)];
        item.style.left = Math.random() * 100 + 'vw';
        item.style.animationDuration = (Math.random() * 2 + 2.5) + 's';
        document.body.appendChild(item);
        setTimeout(() => item.remove(), 3500);
      }, 400);

      // เสียงพูดภาษาไทย
      if ('speechSynthesis' in window) {
        setTimeout(() => {
          const msg = new SpeechSynthesisUtterance('คิดถึงจะแย่แล้ว');
          msg.lang = 'th-TH';
          msg.pitch = 1.3; /* เสียงอ้อนๆ นิดนึง */
          msg.rate = 0.85; /* พูดช้าลงนุ่มๆ */
          window.speechSynthesis.speak(msg);
        }, 300);
      }
    }
  </script>
</body>
</html>
