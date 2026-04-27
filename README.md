<!DOCTYPE html>
<html>
<head>
  <title>Money by God</title>
  <style>
    body { font-family: Arial; background:#111; color:#fff; text-align:center; }
    .box { margin:50px auto; padding:20px; width:300px; background:#222; border-radius:10px; }
    input, button { margin:10px; padding:10px; width:90%; border:none; border-radius:5px; }
    button { background:green; color:white; cursor:pointer; }
  </style>
</head>
<body>

<h1>💰 Money by God</h1>

<div class="box" id="auth">
  <h3>Login / Register</h3>
  <input type="text" id="username" placeholder="Username">
  <button onclick="login()">Enter</button>
</div>

<div class="box" id="dashboard" style="display:none;">
  <h3>Welcome <span id="user"></span></h3>
  <p>Wallet Balance: ₹<span id="balance"></span></p>

  <button onclick="earn()">🎁 Daily Bonus</button>
  <button onclick="withdraw()">💸 Withdraw</button>
  <button onclick="logout()">Logout</button>
</div>

<script>
let balance = 0;

function login(){
  let user = document.getElementById("username").value;
  if(user == "") return alert("Enter username");

  localStorage.setItem("user", user);

  if(!localStorage.getItem("balance")){
    balance = 10; // signup bonus
    localStorage.setItem("balance", balance);
  }

  showDashboard();
}

function showDashboard(){
  document.getElementById("auth").style.display = "none";
  document.getElementById("dashboard").style.display = "block";

  document.getElementById("user").innerText = localStorage.getItem("user");
  document.getElementById("balance").innerText = localStorage.getItem("balance");
}

function earn(){
  balance = parseInt(localStorage.getItem("balance")) + 5;
  localStorage.setItem("balance", balance);
  showDashboard();
}

function withdraw(){
  let bal = parseInt(localStorage.getItem("balance"));

  if(bal < 100){
    alert("Minimum ₹100 required for withdraw");
  } else {
    alert("Withdraw request sent (Demo)");
    localStorage.setItem("balance", 0);
    showDashboard();
  }
}

function logout(){
  location.reload();
}

if(localStorage.getItem("user")){
  showDashboard();
}
</script>

</body>
</html>
