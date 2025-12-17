# Al-Dilwar-OTC-Master
Binary option otc market signal generator ai-dilwar-signal-generator
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>AI Dilwar OTC Master</title>
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
body{margin:0;font-family:Arial;background:#020617;color:#fff}
.hidden{display:none}

/* LOGIN */
.login{
  height:100vh;display:flex;align-items:center;justify-content:center;
}
.box{
  width:360px;background:#0b1f3a;padding:22px;border-radius:16px;
  box-shadow:0 0 35px #22c55e55;text-align:center
}
input,select{
  width:100%;padding:12px;margin:8px 0;border-radius:8px;
  border:none;background:#020617;color:#fff
}
button{
  width:100%;padding:12px;border:none;border-radius:8px;
  background:#22c55e;font-weight:bold;cursor:pointer
}

/* DASHBOARD */
.menu{
  width:220px;height:100vh;background:#020617;
  position:fixed;left:0;top:0;padding:15px
}
.menu h3{color:#22c55e}
.menu a{
  display:block;padding:10px;color:#cbd5f5;text-decoration:none
}
.menu a:hover{background:#0b1f3a}

.main{
  margin-left:220px;padding:20px
}
.card{
  background:#0b1f3a;padding:15px;border-radius:10px;
  margin-bottom:15px
}
.signal{
  font-size:28px;font-weight:bold;margin-top:10px
}
.call{color:#22c55e}
.put{color:#ef4444}
.wait{color:#facc15}
</style>
</head>

<body>

<!-- LOGIN PAGE -->
<div class="login" id="loginPage">
  <div class="box">
    <h2>AI Dilwar OTC Master</h2>
    <input id="uid" placeholder="User ID" value="DilwarAI">
    <input id="pwd" type="password" placeholder="Password" value="848654">
    <button onclick="login()">LOGIN</button>
  </div>
</div>

<!-- DASHBOARD -->
<div id="dashboard" class="hidden">

  <!-- SIDE MENU -->
  <div class="menu">
    <h3>☰ Menu</h3>
    <a href="#">Dashboard</a>
    <a href="#">Signals</a>
    <a href="#">History</a>
    <a href="#" id="adminMenu" onclick="togglePass()">🔐 Change Password</a>
    <a href="#" onclick="logout()">Logout</a>
  </div>

  <!-- MAIN -->
  <div class="main">

    <div class="card">
      <h2>OTC Signal Panel</h2>

      <!-- TIMEFRAME -->
      <label>⏱ Select Timeframe</label>
      <select id="timeframe">
        <option value="30">30 Second</option>
        <option value="60" selected>1 Minute (Default)</option>
        <option value="120">2 Minute</option>
        <option value="180">3 Minute</option>
        <option value="300">5 Minute</option>
      </select>

      <button onclick="generateSignal()">Generate Signal</button>

      <div id="signal" class="signal wait">WAIT</div>
      <div id="conf">Confidence: --%</div>
    </div>

    <!-- CHANGE PASSWORD (ADMIN ONLY) -->
    <div class="card hidden" id="passBox">
      <h3>Change Password (Owner Only)</h3>
      <input id="oldp" type="password" placeholder="Old Password">
      <input id="newp" type="password" placeholder="New Password">
      <button onclick="changePass()">Update Password</button>
    </div>

  </div>
</div>

<script>
/* DEFAULT OWNER */
if(!localStorage.pass){
  localStorage.user="DilwarAI";
  localStorage.pass="848654";
}

let currentUser="";

function login(){
  if(uid.value===localStorage.user && pwd.value===localStorage.pass){
    currentUser=uid.value;
    loginPage.classList.add("hidden");
    dashboard.classList.remove("hidden");

    if(currentUser!=="DilwarAI"){
      adminMenu.style.display="none";
    }
  }else{
    alert("Wrong ID or Password");
  }
}

function logout(){location.reload();}

function togglePass(){
  passBox.classList.toggle("hidden");
}

function changePass(){
  if(oldp.value!==localStorage.pass){
    alert("Old password wrong");return;
  }
  localStorage.pass=newp.value;
  alert("Password Updated");
  oldp.value=newp.value="";
}

/* SIGNAL DEMO LOGIC */
function generateSignal(){
  const tf=document.getElementById("timeframe").value;
  const r=Math.random();

  if(r>0.6){
    signal.className="signal call";
    signal.innerText="CALL";
    conf.innerText="Confidence: 85%";
  }else if(r<0.3){
    signal.className="signal put";
    signal.innerText="PUT";
    conf.innerText="Confidence: 82%";
  }else{
    signal.className="signal wait";
    signal.innerText="WAIT";
    conf.innerText="Confidence: --%";
  }
}
</script>

</body>
</html>
