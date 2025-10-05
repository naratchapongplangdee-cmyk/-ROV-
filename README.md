<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>เติมเกม ROV สุดคุ้ม!</title>
  <link href="https://fonts.googleapis.com/css2?family=Kanit:wght@400;600;700&display=swap" rel="stylesheet" />
  <style>
    :root{
      --bg1:#1a237e;--bg2:#00e5ff;--card:rgba(0,0,0,.7);--text:#fff;--sub:#b3e5fc;
      --accent1:#ff9800;--accent2:#ff3d00;--shadow:#ff980088;--error:#ff5252;--ok:#00c853
    }
    *{box-sizing:border-box}
    body{margin:0;font-family:'Kanit',sans-serif;background:linear-gradient(135deg,var(--bg1) 0%,var(--bg2) 100%);color:var(--text);min-height:100vh;display:flex;flex-direction:column}
    header{text-align:center;padding:2rem 1rem 1rem}
    header img{width:100px;margin-bottom:1rem}
    h1{font-size:2.2rem;margin:0;letter-spacing:1.5px;text-shadow:2px 2px 8px #0008}
    .lead{margin-top:.25rem;opacity:.9}
    .container{width:min(95%,460px);margin:1.25rem auto 2rem;background:var(--card);border-radius:20px;padding:1.5rem;box-shadow:0 8px 32px 0 rgba(31,38,135,.37);backdrop-filter:blur(6px)}
    label{display:block;margin-bottom:.5rem;font-size:1.05rem}
    input,select{width:100%;padding:.8rem .9rem;margin-bottom:1rem;border:none;border-radius:10px;font-size:1rem;background:#f6f8ff;color:#111}
    input::placeholder{color:#777}
    .row{display:grid;grid-template-columns:1fr;gap:1rem}
    @media(min-width:520px){.row{grid-template-columns:1fr 1fr}}
    button{width:100%;padding:.95rem;background:linear-gradient(90deg,var(--accent1) 0%,var(--accent2) 100%);color:#fff;border:none;border-radius:12px;font-size:1.15rem;font-weight:700;cursor:pointer;box-shadow:0 4px 14px var(--shadow);transition:transform .08s ease,filter .2s}
    button:hover{filter:brightness(1.05)}
    button:active{transform:translateY(1px)}
    .helper{color:var(--sub);font-size:.95rem;text-align:center;margin-top:.5rem}
    .footer{text-align:center;margin:1rem 0 2rem;color:var(--sub);font-size:.95rem}
    .footer .copy{display:inline-flex;gap:.5rem;align-items:center;border:1px solid #ffffff33;border-radius:999px;padding:.35rem .75rem}

    /* error text */
    .err{color:var(--error);font-size:.9rem;margin:-.5rem 0 .75rem}
    .hidden{display:none!important}

    /* modal */
    .modal-backdrop{position:fixed;inset:0;background:rgba(0,0,0,.6);display:flex;align-items:center;justify-content:center;padding:1rem;z-index:50}
    .modal{width:min(560px,95vw);background:#0b1024;border:1px solid #ffffff22;border-radius:18px;box-shadow:0 20px 80px #000a}
    .modal header{padding:1rem 1.25rem 0}
    .modal h2{font-size:1.4rem;margin:.25rem 0}
    .modal .content{padding:0 1.25rem 1rem}
    .summary{background:#0f1633;border:1px solid #ffffff14;border-radius:14px;padding:1rem;display:grid;gap:.5rem;margin:.5rem 0 1rem}
    .summary div{display:flex;justify-content:space-between;gap:1rem}
    .summary .key{opacity:.85}
    .actions{display:grid;grid-template-columns:1fr 1fr;gap:.75rem}
    .btn-outline{background:transparent;border:1px solid #ffffff44}

    /* toast */
    .toast{position:fixed;bottom:20px;left:50%;transform:translateX(-50%);background:#0b1024;border:1px solid #ffffff33;color:#fff;padding:.75rem 1rem;border-radius:12px;box-shadow:0 10px 30px #000a;opacity:0;pointer-events:none;transition:opacity .25s ease;z-index:60}
    .toast.show{opacity:1}
  </style>
</head>
<body>
  <header>
    <img src="https://static.wikia.nocookie.net/arenaofvalor_gamepedia/images/7/7e/ROV_Logo.png" alt="ROV Logo" />
    <h1>เติมเกม ROV สุดคุ้ม!</h1>
    <p class="lead">ปลอดภัย รวดเร็ว ได้รับโค้ดทันที</p>
  </header>

  <div class="container">
    <form id="topupForm" novalidate>
      <label for="playerid">Player ID</label>
      <input type="text" id="playerid" name="playerid" placeholder="กรอกไอดีเกมของคุณ" required />
      <div id="err-playerid" class="err hidden">กรุณากรอก Player ID</div>

      <div class="row">
        <div>
          <label for="amount">เลือกจำนวนคูปอง</label>
          <select id="amount" name="amount" required>
            <option value="">-- เลือกจำนวน --</option>
            <option value="50">50 คูปอง - 35 บาท</option>
            <option value="100">100 คูปอง - 65 บาท</option>
            <option value="300">300 คูปอง - 190 บาท</option>
            <option value="500">500 คูปอง - 310 บาท</option>
          </select>
          <div id="err-amount" class="err hidden">กรุณาเลือกจำนวนคูปอง</div>
        </div>
        <div>
          <label for="payment">ช่องทางชำระเงิน</label>
          <select id="payment" name="payment" required>
            <option value="">-- เลือกช่องทาง --</option>
            <option value="truemoney">TrueMoney Wallet</option>
            <option value="promptpay">PromptPay</option>
            <option value="bank">โอนผ่านธนาคาร</option>
          </select>
          <div id="err-payment" class="err hidden">กรุณาเลือกช่องทางชำระเงิน</div>
        </div>
      </div>

      <button type="submit">เติมคูปองเลย!</button>
      <div class="helper">กดปุ่มเพื่อดูสรุปคำสั่งซื้อก่อนยืนยันการชำระเงินจริง</div>
    </form>
  </div>

  <div class="footer">
    &copy; 2024 เติมเกม ROV | บริการ 24 ชั่วโมง | ติดต่อแอดมิน Line: <span class="copy" id="lineCopy">@rovshop</span>
  </div>

  <!-- Modal -->
  <div id="backdrop" class="modal-backdrop hidden" role="dialog" aria-modal="true" aria-labelledby="summaryTitle">
    <div class="modal">
      <header>
        <h2 id="summaryTitle">สรุปคำสั่งซื้อ</h2>
      </header>
      <div class="content">
        <div class="summary" id="summaryBox">
          <!-- filled by JS -->
        </div>
        <div class="actions">
          <button id="cancelBtn" class="btn-outline">แก้ไขรายการ</button>
          <button id="confirmBtn">ยืนยันและชำระเงิน</button>
        </div>
        <p class="helper" id="paymentHint"></p>
      </div>
    </div>
  </div>

  <!-- Toast -->
  <div id="toast" class="toast" role="status" aria-live="polite"></div>

  <script>
    // ราคาอ้างอิงจากจำนวนคูปอง
    const PRICE_TABLE = {"50":35,"100":65,"300":190,"500":310};

    const form = document.getElementById('topupForm');
    const playerEl = document.getElementById('playerid');
    const amountEl = document.getElementById('amount');
    const payEl = document.getElementById('payment');

    const errPlayer = document.getElementById('err-playerid');
    const errAmount = document.getElementById('err-amount');
    const errPayment = document.getElementById('err-payment');

    const backdrop = document.getElementById('backdrop');
    const summaryBox = document.getElementById('summaryBox');
    const paymentHint = document.getElementById('paymentHint');
    const cancelBtn = document.getElementById('cancelBtn');
    const confirmBtn = document.getElementById('confirmBtn');
    const toast = document.getElementById('toast');

    const lineCopy = document.getElementById('lineCopy');
    lineCopy.addEventListener('click', async ()=>{
      try{await navigator.clipboard.writeText('@rovshop');showToast('คัดลอกไลน์ @rovshop แล้ว');}catch{showToast('คัดลอกไม่สำเร็จ');}
    });

    function showToast(msg){
      toast.textContent = msg; toast.classList.add('show');
      setTimeout(()=> toast.classList.remove('show'), 1800);
    }

    function validate(){
      let ok = true;
      const pid = playerEl.value.trim();
      if(!pid){errPlayer.classList.remove('hidden'); ok=false} else {errPlayer.classList.add('hidden')}
      if(!amountEl.value){errAmount.classList.remove('hidden'); ok=false} else {errAmount.classList.add('hidden')}
      if(!payEl.value){errPayment.classList.remove('hidden'); ok=false} else {errPayment.classList.add('hidden')}
      return ok;
    }

    function openModal(){backdrop.classList.remove('hidden');}
    function closeModal(){backdrop.classList.add('hidden');}

    function formatTHB(num){return new Intl.NumberFormat('th-TH',{style:'currency',currency:'THB'}).format(num)}

    function paymentMethodLabel(v){
      return ({truemoney:'TrueMoney Wallet',promptpay:'PromptPay',bank:'โอนผ่านธนาคาร'})[v] || '-';
    }

    form.addEventListener('submit', (e)=>{
      e.preventDefault();
      if(!validate()) return;

      const pid = playerEl.value.trim();
      const amount = amountEl.value;
      const price = PRICE_TABLE[amount] || 0;
      const pay = payEl.value;

      summaryBox.innerHTML = `
        <div><span class="key">Player ID</span><strong>${escapeHtml(pid)}</strong></div>
        <div><span class="key">จำนวนคูปอง</span><strong>${amount} คูปอง</strong></div>
        <div><span class="key">ราคา</span><strong>${formatTHB(price)}</strong></div>
        <div><span class="key">ชำระผ่าน</span><strong>${paymentMethodLabel(pay)}</strong></div>
      `;

      paymentHint.textContent = pay==='promptpay' ? 'หลังยืนยัน ระบบจะแสดงเลข PromptPay ชั่วคราวสำหรับชำระเงิน'
        : pay==='truemoney' ? 'หลังยืนยัน โปรดส่งสลิป TrueMoney ให้แอดมิน @rovshop'
        : 'หลังยืนยัน จะแสดงเลขบัญชีสำหรับโอนผ่านธนาคาร';

      openModal();
    });

    cancelBtn.addEventListener('click', ()=> closeModal());

    confirmBtn.addEventListener('click', ()=>{
      // จำลองการยืนยันคำสั่งซื้อ (Front-end only)
      closeModal();
      // สร้างหมายเลขออเดอร์สุ่ม
      const order = 'RV' + Math.floor(Math.random()*1e6).toString().padStart(6,'0');
      showToast('ยืนยันออเดอร์ #' + order + ' เรียบร้อย');

      // ตัวอย่าง: ส่งข้อมูลไปยัง endpoint ภายหลัง
      // fetch('/api/order', {method:'POST', headers:{'Content-Type':'application/json'}, body: JSON.stringify({...})});
    });

    // ปรับข้อความ error แบบ realtime เล็กน้อย
    [playerEl, amountEl, payEl].forEach(el=> el.addEventListener('input', validate));

    // ป้องกัน XSS กับค่าที่ผู้ใช้กรอก
    function escapeHtml(str){
      return str.replace(/[&<>'"]/g, (c)=>({"&":"&amp;","<":"&lt;",">":"&gt;","'":"&#39;","\"":"&quot;"}[c]));
    }
  </script>
</body>
</html>
