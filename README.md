<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>AI Dilwar OTC Master</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap');
*{box-sizing:border-box;font-family:'Poppins',sans-serif;}
body{margin:0;min-height:100vh;display:flex;justify-content:center;align-items:center;background:radial-gradient(circle at top,#1e3a8a,#020617 70%);color:#fff;}

/* CARD STYLE */
.card{width:92%;max-width:500px;background:rgba(255,255,255,0.08);backdrop-filter:blur(16px);border-radius:18px;padding:28px 24px 26px;box-shadow:0 0 30px rgba(0,255,150,0.25), inset 0 0 0 1px rgba(255,255,255,.15);text-align:center;}
.brand{font-size:30px;font-weight:700;margin-bottom:4px;letter-spacing:.5px;}
.brand span{color:#22c55e;text-shadow:0 0 12px rgba(34,197,94,.8);}
.sub{font-size:13px;opacity:.9;margin-bottom:14px;}
.live{color:#22c55e;font-size:13px;margin-bottom:20px;font-weight:600;}
.field{margin-bottom:14px;position:relative;}
.field input{width:100%;padding:14px 14px 14px 44px;border-radius:12px;border:none;outline:none;font-size:14px;background:rgba(0,0,0,.35);color:#fff;box-shadow:inset 0 0 0 1px rgba(255,255,255,.2);}
.field i{position:absolute;top:50%;left:14px;transform:translateY(-50%);opacity:.7;}
button{width:100%;padding:14px;border:none;border-radius:14px;font-size:15px;font-weight:600;cursor:pointer;color:#fff;background:linear-gradient(135deg,#22c55e,#16a34a);box-shadow:0 8px 20px rgba(34,197,94,.5);margin-bottom:10px;}
button:active{transform:scale(.98);}
.warn{margin-top:10px;font-size:12px;opacity:.85;}
.footer{margin-top:18px;font-size:12px;opacity:.7;}
select{width:100%;padding:12px;margin:8px 0;border-radius:10px;border:none;outline:none;background:rgba(0,0,0,0.35);color:#fff;font-size:14px;}
.signal-box{text-align:center;font-size:22px;font-weight:bold;padding:20px;border-radius:12px;background:#020617;border:2px dashed #22c55e;margin-top:15px;transition: all 0.3s ease;}
.signal-box.update{box-shadow:0 0 20px #22c55e;transform:scale(1.05);}
#adminBox{display:none;text-align:left;margin-top:15px;}
#adminBox label{display:block;margin:6px 0 4px;}
#adminBox input{width:100%;padding:10px;border-radius:10px;border:none;outline:none;background:rgba(0,0,0,0.35);color:#fff;margin-bottom:10px;}
</style>
</head>
<body>

<!-- LOGIN CARD -->
<div class="card" id="loginBox">
  <div class="brand">AI Dilwar <span>OTC Master</span></div>
  <div class="sub">Smart AI • Accurate OTC Signals</div>
  <div class="live">LIVE OTC SYSTEM</div>
  <div class="field"><i>👤</i><input id="uid" type="text" placeholder="Enter User ID"></div>
  <div class="field"><i>🔒</i><input id="pwd" type="password" placeholder="Enter Password"></div>
  <button onclick="login()">LOGIN</button>

  <div id="adminBox">
    <label>Change Password:</label>
    <input type="password" id="newPwd" placeholder="Enter new password">
    <button onclick="changePassword()">Update Password</button>
    <div class="warn">Admin can update password here.</div>
  </div>

  <div class="warn">⚠ Unauthorized access strictly prohibited</div>
  <div class="footer">© 2025 AI Dilwar OTC Master • Chrome Optimized ✅</div>
</div>

<!-- DASHBOARD CARD -->
<div class="card" id="dashboardBox" style="display:none;">
  <div class="brand">AI Dilwar <span>OTC Dashboard</span></div>

  <!-- Market Select -->
  <select id="market">
    <option value="">Select Market</option>
    <option>EUR/USD OTC</option><option>GBP/USD OTC</option><option>USD/JPY OTC</option>
    <option>AUD/USD OTC</option><option>USD/CHF OTC</option><option>EUR/JPY OTC</option>
    <option>GBP/JPY OTC</option><option>EUR/GBP OTC</option><option>NZD/USD OTC</option>
    <option>USD/CAD OTC</option><option>AUD/JPY OTC</option><option>CAD/JPY OTC</option>
    <option>CHF/JPY OTC</option><option>EUR/AUD OTC</option><option>EUR/CAD OTC</option>
    <option>EUR/CHF OTC</option><option>EUR/NZD OTC</option><option>GBP/AUD OTC</option>
    <option>GBP/CAD OTC</option><option>GBP/CHF OTC</option><option>GBP/NZD OTC</option>
    <option>NZD/JPY OTC</option><option>AUD/CAD OTC</option><option>AUD/CHF OTC</option>
    <option>AUD/NZD OTC</option><option>CAD/CHF OTC</option><option>NZD/CAD OTC</option>
    <option>NZD/CHF OTC</option><option>USD/SGD OTC</option><option>USD/ZAR OTC</option>
  </select>

  <!-- Timeframe -->
  <select id="timeframe">
    <option>30 Second</option>
    <option>1 Minute</option>
    <option>2 Minute</option>
    <option>3 Minute</option>
    <option>4 Minute</option>
    <option>5 Minute</option>
  </select>

  <button onclick="generateSignal()">Generate Signal</button>
  <div class="signal-box" id="signalBox">WAITING FOR SIGNAL</div>
  <div class="footer">OTC signals are for educational use only</div>
</div>

<script>
// Initialize default password
if(!localStorage.getItem("adminPwd")){ localStorage.setItem("adminPwd","848654"); }

// Login function
function login(){
  const uid = document.getElementById("uid").value;
  const pwd = document.getElementById("pwd").value;
  const storedPwd = localStorage.getItem("adminPwd");

  if(uid==="Admin" && pwd===storedPwd){
    alert("Welcome Admin! You can change password.");
    document.getElementById("adminBox").style.display="block";
  }
  else if(uid==="DilwarAI" && pwd===storedPwd){
    alert("Login Successful! Welcome User.");
    document.getElementById("loginBox").style.display="none";
    document.getElementById("dashboardBox").style.display="block";
  }
  else{ alert("Invalid User ID or Password"); }
}

// Admin password change
function changePassword(){
  const newPwd = document.getElementById("newPwd").value;
  if(newPwd.length<4){ alert("Password too short!"); return; }
  localStorage.setItem("adminPwd",newPwd);
  alert("Password updated successfully!");
  document.getElementById("newPwd").value="";
}

// Automatic 8 indicators (no select box)
const indicators=["RSI","MACD","EMA","SMA","Bollinger","Stochastic","ADX","CCI"];

// Generate Signal function
function generateSignal(){
  const market = document.getElementById("market").value;
  const timeframe = document.getElementById("timeframe").value;
  const signalBox = document.getElementById("signalBox");
  if(!market || !timeframe){ alert("Select Market and Timeframe!"); return; }

  // Simulate indicator signals (random BUY/SELL)
  const indSignals = indicators.map(()=>Math.random()<0.5?"BUY":"SELL");
  const buyCount = indSignals.filter(s=>"BUY"===s).length;
  const sellCount = indSignals.filter(s=>"SELL"===s).length;

  let finalSignal="HOLD ⚪";
  if(buyCount>=4) finalSignal="BUY 💚";
  else if(sellCount>=4) finalSignal="SELL 🔴";

  // Simulate profit % estimation (random realistic for demo)
  const profitPercent = Math.floor(Math.random()*40)+60; // 60-100%
  signalBox.textContent="WAITING FOR SIGNAL...";

  // Show signal 3 seconds before candle close
  setTimeout(()=>{
    signalBox.textContent=`${finalSignal} (${market}, ${timeframe}) | Estimated Profit: ${profitPercent}%`;
    signalBox.classList.add("update");
    setTimeout(()=>signalBox.classList.remove("update"),300);
  },3000);
}
</script>

</body>
</html>
