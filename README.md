<!DOCTYPE html>
<html lang="my">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>မင်းအတွက် စာလေးတစ်စောင် 💖</title>
  <style>
    * {
      box-sizing: border-box;
    }
    body {
      margin: 0;
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      background: linear-gradient(135deg, #ff758c 0%, #ff7eb3 50%, #ffb199 100%);
      font-family: -apple-system, BlinkMacSystemFont, "Pyidaungsu", "Myanmar Text", sans-serif;
      color: #fff;
      text-align: center;
      padding: 20px;
      overflow: hidden;
    }
    .card {
      background: rgba(255, 255, 255, 0.22);
      backdrop-filter: blur(12px);
      -webkit-backdrop-filter: blur(12px);
      border: 1px solid rgba(255, 255, 255, 0.35);
      padding: 30px 22px;
      border-radius: 24px;
      width: 100%;
      max-width: 370px;
      box-shadow: 0 12px 32px rgba(214, 51, 108, 0.25);
      position: relative;
    }
    img.gif-box {
      width: 160px;
      height: 160px;
      object-fit: contain;
      border-radius: 16px;
      margin-bottom: 14px;
    }
    h2 {
      margin: 8px 0 12px;
      font-size: 22px;
      line-height: 1.5;
      text-shadow: 0 2px 6px rgba(0, 0, 0, 0.15);
    }
    p.sub-text {
      font-size: 15px;
      margin: 0 0 22px;
      opacity: 0.95;
      line-height: 1.6;
    }
    .btns {
      display: flex;
      justify-content: center;
      align-items: center;
      gap: 14px;
      margin-top: 10px;
      min-height: 55px;
    }
    button {
      border: none;
      padding: 12px 24px;
      border-radius: 14px;
      font-size: 16px;
      font-weight: bold;
      cursor: pointer;
      transition: transform 0.18s ease, background 0.2s ease;
      font-family: inherit;
    }
    #yesBtn {
      background: #ff1e56;
      color: #fff;
      box-shadow: 0 6px 16px rgba(255, 30, 86, 0.4);
      z-index: 10;
    }
    #noBtn {
      background: #4a4e69;
      color: #fff;
      position: relative;
      z-index: 20;
    }
    #successBox {
      display: none;
      animation: popIn 0.4s ease;
    }
    @keyframes popIn {
      0% { transform: scale(0.8); opacity: 0; }
      100% { transform: scale(1); opacity: 1; }
    }
    .hearts {
      font-size: 28px;
      margin-top: 12px;
      letter-spacing: 6px;
    }
  </style>
</head>
<body>

  <!-- အဖြေတောင်းသည့် အပိုင်း -->
  <div class="card" id="questionBox">
    <img class="gif-box" src="https://media.tenor.com/gUiu1zyxfzYAAAAi/bear-kiss-bear-kisses.gif" alt="Cute Bear" />
    <h2 id="questionText">ကိုယ့်ကို ချစ်လားဟင်? 🥺</h2>
    <p class="sub-text" id="subText">အမှန်အတိုင်းလေး ဖြေပေးနော်...</p>
    <div class="btns">
      <button id="yesBtn">ချစ်တယ် 💖</button>
      <button id="noBtn">မချစ်ဘူး</button>
    </div>
  </div>

  <!-- ချစ်တယ် နှိပ်လိုက်ရင် ပေါ်လာမည့် အပိုင်း -->
  <div class="card" id="successBox">
    <img class="gif-box" src="https://media.tenor.com/1d1xQ6o5G-QAAAAi/milk-and-mocha-bear-couple.gif" alt="Happy Bears" />
    <h2>ရေး... အရမ်းပျော်တာပဲ! 🎉</h2>
    <p class="sub-text">
      ဒီနေ့ကစပြီး ကိုယ့်ဘဝရဲ့ အပျော်ရွှင်ရဆုံးနေ့လေး ဖြစ်သွားပါပြီ။ 
      အမြဲတမ်း ဂရုစိုက်ပြီး ချစ်သွားပါ့မယ်နော် ❤️
    </p>
    <div class="hearts">💖 💕 💗</div>
  </div>

  <script>
    const noBtn = document.getElementById("noBtn");
    const yesBtn = document.getElementById("yesBtn");
    const questionText = document.getElementById("questionText");
    const subText = document.getElementById("subText");
    const questionBox = document.getElementById("questionBox");
    const successBox = document.getElementById("successBox");

    const teaseMessages = [
      { title: "သေချာလို့လားဟင်? 🥺", sub: "သေချာပြန်စဉ်းစားပါဦးနော်..." },
      { title: "မချစ်ဘူး မနှိပ်ပါနဲ့ 😭", sub: "ကိုယ် အသည်းကွဲသွားလိမ့်မယ်!" },
      { title: "ဒီခလုတ်က နှိပ်လို့မရဘူး 😜", sub: "ဟိုဘက်က အနီရောင်လေးပဲ နှိပ်လို့ရတာ" },
      { title: "မရဘူးကွာ ချစ်တယ်လို့ပဲ နှိပ် ❤️", sub: "ကိုယ် မင်းကို အရမ်းချစ်တာ သိရဲ့သားနဲ့" },
      { title: "လက်ညှိုးလေး နည်းနည်းရွှေ့လိုက်ပါဦး 😊", sub: "ဘေးက ခလုတ်အကြီးကြီးကို မြင်တယ်မလား?" }
    ];

    let count = 0;
    let yesScale = 1;

    function moveNoButton() {
      noBtn.style.position = "fixed";
      const padding = 24;
      const maxX = window.innerWidth - noBtn.offsetWidth - padding;
      const maxY = window.innerHeight - noBtn.offsetHeight - padding;

      const randomX = Math.max(padding, Math.floor(Math.random() * maxX));
      const randomY = Math.max(padding, Math.floor(Math.random() * maxY));

      noBtn.style.left = randomX + "px";
      noBtn.style.top = randomY + "px";

      const currentMsg = teaseMessages[count % teaseMessages.length];
      questionText.textContent = currentMsg.title;
      subText.textContent = currentMsg.sub;
      count++;

      yesScale = Math.min(yesScale + 0.14, 1.9);
      yesBtn.style.transform = `scale(${yesScale})`;
    }

    noBtn.addEventListener("pointerdown", (e) => {
      e.preventDefault();
      moveNoButton();
    });
    noBtn.addEventListener("mouseover", moveNoButton);

    yesBtn.addEventListener("click", () => {
      noBtn.style.display = "none";
      questionBox.style.display = "none";
      successBox.style.display = "block";
    });
  </script>
</body>
</html>
