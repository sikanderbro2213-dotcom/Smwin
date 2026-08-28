<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SIMA Coin Hub</title>
    
    <!-- Monetag Zone Ad SDK -->
    <script src='//libtl.com/sdk.js' data-zone='11669909' data-sdk='show_11669909'></script>

    <style>
        body { font-family: 'Poppins', sans-serif; background: #0b0b0e; color: #fff; text-align: center; margin: 0; padding: 0; user-select: none; }
        .container { max-width: 400px; margin: 0 auto; background: #12121a; min-height: 100vh; position: relative; box-shadow: 0 0 20px rgba(0,0,0,0.8); display: flex; flex-direction: column; }
        
        .auth-box { padding: 30px 20px; }
        .app-box { display: none; flex: 1; padding: 20px; padding-bottom: 80px; }
        
        .top-bar { display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid #222; padding-bottom: 10px; }
        .user-id { font-size: 12px; color: #ffd700; font-weight: bold; }
        .logout-btn { background: #e74c3c; color: white; border: none; padding: 5px 12px; border-radius: 6px; cursor: pointer; font-size: 11px; font-weight: bold; }

        .balance-box { font-size: 36px; font-weight: 800; color: #ffd700; margin: 25px 0 10px 0; text-shadow: 0 0 15px rgba(255, 215, 0, 0.4); }
        
        .coin-container { flex: 1; display: flex; justify-content: center; align-items: center; margin: 30px 0; }
        .coin-wrapper { position: relative; display: inline-block; }
        .coin-btn {
            width: 180px; height: 180px; border-radius: 50%; background: radial-gradient(circle, #ffe066 0%, #f39c12 100%);
            border: 8px solid #fff; color: #12121a; font-size: 100px; font-weight: 900; cursor: pointer;
            box-shadow: 0 0 35px rgba(255, 215, 0, 0.5); transition: transform 0.05s; display: flex; align-items: center; justify-content: center;
        }
        .coin-btn:active { transform: scale(0.92); }

        .float-text { position: absolute; color: #ffd700; font-weight: bold; font-size: 22px; animation: floatUp 0.8s forwards; pointer-events: none; }
        @keyframes floatUp { 0% { opacity: 1; transform: translateY(0); } 100% { opacity: 0; transform: translateY(-60px); } }

        .bottom-nav { position: absolute; bottom: 0; left: 0; right: 0; background: #1a1a26; display: flex; border-top: 1px solid #2a2a3a; height: 60px; }
        .tab-btn { flex: 1; background: none; border: none; color: #888; font-size: 10px; font-weight: bold; cursor: pointer; display: flex; flex-direction: column; align-items: center; justify-content: center; }
        .tab-btn.active { color: #ffd700; }
        .tab-btn span { font-size: 18px; margin-bottom: 2px; }

        .view { display: none; text-align: left; }
        .view.active { display: block; }
        
        input, select { width: 100%; padding: 12px; margin: 8px 0; border-radius: 8px; border: 1px solid #333; background: #1a1a26; color: #fff; box-sizing: border-box; }
        .action-btn { width: 100%; padding: 12px; background: #ffd700; color: #000; border: none; font-weight: bold; border-radius: 8px; cursor: pointer; margin-top: 10px; }
        .action-btn:disabled { background: #555 !important; color: #888 !important; cursor: not-allowed; }
        .card { background: #1a1a26; padding: 15px; border-radius: 10px; border: 1px solid #2a2a3a; margin-bottom: 12px; }
        
        .profile-avatar { width: 70px; height: 70px; border-radius: 50%; background: #ffd700; color: #12121a; font-size: 32px; font-weight: bold; display: flex; align-items: center; justify-content: center; margin: 10px auto; border: 3px solid #fff; }
        .stat-row { display: flex; justify-content: space-between; border-bottom: 1px solid #2a2a3a; padding: 10px 0; font-size: 13px; }
        
        #banScreen { display: none; padding: 60px 20px; color: #e74c3c; text-align: center; }
    </style>
</head>
<body>

<div class="container">
    <!-- Ban Screen -->
    <div id="banScreen">
        <h2>🚫 ACCOUNT BANNED</h2>
        <p style="color:#aaa; font-size: 13px;">Aapka account suspend kar diya gaya hai.</p>
        <button class="action-btn" style="background:#e74c3c; color:#fff;" onclick="logout()">LOGOUT</button>
    </div>

    <!-- Auth Screen -->
    <div id="authBox" class="auth-box">
        <h2 style="color:#ffd700;">🪙 SIMA Coin</h2>
        <input type="text" id="usernameInput" placeholder="Username">
        <input type="password" id="passwordInput" placeholder="Password">
        <button class="action-btn" onclick="handleAuth('login')">LOGIN</button>
        <button class="action-btn" style="background: #27ae60; color: #fff;" onclick="handleAuth('register')">CREATE ACCOUNT</button>
    </div>

    <!-- App Screen -->
    <div id="appBox" class="app-box">
        <div class="top-bar">
            <span class="user-id" id="userIdDisplay">User: -</span>
            <button class="logout-btn" onclick="logout()">Logout</button>
        </div>

        <!-- 1. HOME TAB -->
        <div id="tabHome" class="view active" style="text-align: center;">
            <div class="balance-box"><span id="balance">0.00000</span> <span style="font-size: 18px;">SIMA</span></div>
            <div class="coin-container">
                <div class="coin-wrapper" id="coinWrapper">
                    <div class="coin-btn" onclick="tapCoin(event)">S</div>
                </div>
            </div>
        </div>

        <!-- 2. GAMES & MINING TAB -->
        <div id="tabGames" class="view">
            <h3 style="color:#ffd700;">🎮 Mini Games & Mining</h3>
            
            <div class="card">
                <h4>📺 Watch Ads (Daily: <span id="adCountDisplay">0</span>/20)</h4>
                <p style="font-size: 11px; color: #aaa;">Earn 1.00000 SIMA per ad.</p>
                <button id="adBtn" class="action-btn" style="background: #9b59b6; color: white;" onclick="watchAd()">WATCH AD NOW</button>
            </div>

            <div class="card">
                <h4>🎫 Daily Scratch Card</h4>
                <p id="scratchResult" style="color: #2ecc71; font-weight: bold; font-size: 12px;">Get 1 free card every 24 hours!</p>
                <button id="scratchBtn" class="action-btn" style="background: #e67e22; color: white;" onclick="scratchCard()">SCRATCH NOW</button>
            </div>

            <div class="card">
                <h4>🎰 Spin & Win</h4>
                <p id="spinResult" style="color: #2ecc71; font-weight: bold; font-size: 12px;">Cost: 5.00000 SIMA</p>
                <button class="action-btn" onclick="spinWheel()">SPIN WHEEL</button>
            </div>

            <div class="card">
                <h4>⚡ Auto SIMA Miner</h4>
                <p id="minerStatus" style="font-size: 12px; color: #aaa;">Cost: 20 SIMA (+0.0001/sec)</p>
                <button class="action-btn" style="background: #3498db; color: white;" onclick="buyMiner()">BUY MINER</button>
            </div>
        </div>

        <!-- 3. WALLET TAB -->
        <div id="tabWallet" class="view">
            <h3 style="color:#ffd700;">🏧 Wallet & Refer</h3>
            
            <div class="card">
                <h4>👥 Invite Friends</h4>
                <input type="text" id="referLink" readonly>
            </div>

            <div class="card">
                <h4>🏧 Withdraw SIMA (Instant)</h4>
                <select id="method">
                    <option value="UPI">UPI ID</option>
                    <option value="PayPal">PayPal Email</option>
                    <option value="Crypto">Crypto Wallet Address</option>
                </select>
                <input type="number" id="withdrawAmount" placeholder="Enter Amount (Min: 50 SIMA)" min="50">
                <input type="text" id="walletInput" placeholder="Enter Address / ID">
                <button class="action-btn" style="background: #27ae60; color: white;" onclick="submitWithdraw()">WITHDRAW INSTANTLY</button>
            </div>
        </div>

        <!-- 4. PROFILE TAB -->
        <div id="tabProfile" class="view">
            <h3 style="color:#ffd700;">👤 Player Profile</h3>
            
            <div class="card" style="text-align: center;">
                <div class="profile-avatar" id="avatarInitial">U</div>
                <h3 id="profileUsername" style="margin: 5px 0; color: #fff; border:none;">Player ID</h3>
                <span style="font-size: 11px; background: #27ae60; padding: 2px 8px; border-radius: 10px;">VERIFIED PLAYER</span>
            </div>

            <div class="card">
                <h4>📊 Account Statistics</h4>
                <div class="stat-row">
                    <span>Total Balance:</span>
                    <strong style="color:#ffd700;" id="profBalance">0.00000 SIMA</strong>
                </div>
                <div class="stat-row">
                    <span>Ads Watched Today:</span>
                    <strong id="profAds">0/20</strong>
                </div>
                <div class="stat-row">
                    <span>Auto Miner Status:</span>
                    <strong id="profMiner" style="color:#e74c3c;">Inactive</strong>
                </div>
            </div>

            <div class="card">
                <h4>⚙️ Account Actions</h4>
                <button class="action-btn" style="background: #e74c3c; color: white;" onclick="logout()">LOGOUT ACCOUNT</button>
            </div>
        </div>

        <!-- Bottom Navigation -->
        <div class="bottom-nav">
            <button class="tab-btn active" onclick="switchTab('tabHome', this)"><span>🪙</span> Tap</button>
            <button class="tab-btn" onclick="switchTab('tabGames', this)"><span>🎮</span> Games</button>
            <button class="tab-btn" onclick="switchTab('tabWallet', this)"><span>💳</span> Wallet</button>
            <button class="tab-btn" onclick="switchTab('tabProfile', this)"><span>👤</span> Profile</button>
        </div>
    </div>
</div>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
  import { getDatabase, ref, set, get, child, runTransaction } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

  const firebaseConfig = {
    apiKey: "AIzaSyCovJTwaxhR6Gc-w50-_pes3Ux-2PTbfBE",
    authDomain: "simu-fefe9.firebaseapp.com",
    databaseURL: "https://simu-fefe9-default-rtdb.firebaseio.com",
    projectId: "simu-fefe9",
    storageBucket: "simu-fefe9.firebasestorage.app",
    messagingSenderId: "635175753881",
    appId: "1:635175753881:web:f88095bfa9e8dfda660008",
    measurementId: "G-NJPQ3BHN7R"
  };

  const app = initializeApp(firebaseConfig);
  const db = getDatabase(app);

  let currentUsername = localStorage.getItem('sima_username');
  let minerActive = false;
  let adCount = 0;
  let lastAdReset = Date.now();
  let lastScratchTime = 0;

  if (currentUsername) loadUserData(currentUsername);

  window.handleAuth = async function(type) {
      const user = document.getElementById('usernameInput').value.trim().toLowerCase();
      const pass = document.getElementById('passwordInput').value.trim();
      if (!user || !pass) return alert("Fill all fields!");

      const snapshot = await get(child(ref(db), `users/${user}`));
      if (type === 'register') {
          if (snapshot.exists()) alert("Username taken!");
          else {
              await set(ref(db, 'users/' + user), { 
                  password: pass, 
                  balance: 0.00000, 
                  miner: false, 
                  adCount: 0, 
                  lastAdReset: Date.now(),
                  lastScratchTime: 0,
                  banned: false
              });
              loginSuccess(user);
          }
      } else if (type === 'login') {
          if (snapshot.exists() && snapshot.val().password === pass) loginSuccess(user);
          else alert("Wrong Login!");
      }
  };

  function loginSuccess(user) {
      localStorage.setItem('sima_username', user);
      currentUsername = user;
      loadUserData(user);
  }

  function loadUserData(user) {
      get(child(ref(db), `users/${user}`)).then((snapshot) => {
          if (snapshot.exists()) {
              let val = snapshot.val();
              
              if (val.banned) {
                  document.getElementById("authBox").style.display = "none";
                  document.getElementById("appBox").style.display = "none";
                  document.getElementById("banScreen").style.display = "block";
                  return;
              }

              document.getElementById("authBox").style.display = "none";
              document.getElementById("appBox").style.display = "flex";
              document.getElementById("userIdDisplay").innerText = "User: " + user;
              document.getElementById("referLink").value = "Refer Code: " + user;

              document.getElementById("profileUsername").innerText = user.toUpperCase();
              document.getElementById("avatarInitial").innerText = user.charAt(0).toUpperCase();

              window.simaBalance = val.balance || 0;
              adCount = val.adCount || 0;
              lastAdReset = val.lastAdReset || Date.now();
              lastScratchTime = val.lastScratchTime || 0;

              if (Date.now() - lastAdReset > 24 * 60 * 60 * 1000) {
                  adCount = 0;
                  lastAdReset = Date.now();
                  set(ref(db, `users/${user}/adCount`), 0);
                  set(ref(db, `users/${user}/lastAdReset`), lastAdReset);
              }

              if (val.miner) startMining();
              updateDisplay();
              checkScratchAvailability();
          }
      });
  }

  window.watchAd = function() {
      if (adCount >= 20) return alert("Daily 20 Ads limit completed!");

      const adBtn = document.getElementById("adBtn");
      adBtn.innerText = "Loading Ad...";
      adBtn.disabled = true;

      const triggerAd = () => {
          if (typeof window.show_11669909 === 'function') {
              window.show_11669909().then(() => {
                  adCount++;
                  updateDBBalance(1.00000);
                  set(ref(db, `users/${currentUsername}/adCount`), adCount);
                  alert("🎉 Reward Received: +1.00000 SIMA!");
                  resetAdBtn();
              }).catch(() => {
                  alert("Ad interrupted.");
                  resetAdBtn();
              });
          } else {
              alert("Ad script loading/blocked. Retry.");
              resetAdBtn();
          }
      };

      setTimeout(triggerAd, 400);

      function resetAdBtn() {
          if (adBtn) {
              adBtn.innerText = "WATCH AD NOW";
              adBtn.disabled = adCount >= 20;
          }
      }
  };

  function checkScratchAvailability() {
      let now = Date.now();
      let timePassed = now - lastScratchTime;
      let dayMs = 24 * 60 * 60 * 1000;

      let scratchBtn = document.getElementById("scratchBtn");
      let scratchResult = document.getElementById("scratchResult");

      if (timePassed < dayMs) {
          scratchBtn.disabled = true;
          let hoursLeft = Math.ceil((dayMs - timePassed) / (1000 * 60 * 60));
          scratchResult.innerText = `⏳ Next scratch in ${hoursLeft} Hours!`;
      } else {
          scratchBtn.disabled = false;
          scratchResult.innerText = "🎁 Scratch Card Available!";
      }
  }

  window.scratchCard = function() {
      let now = Date.now();
      if (now - lastScratchTime < 24 * 60 * 60 * 1000) return alert("Daily limit reached!");

      let reward = (Math.random() * 0.5 + 0.1).toFixed(5);
      updateDBBalance(parseFloat(reward));
      
      lastScratchTime = now;
      set(ref(db, `users/${currentUsername}/lastScratchTime`), lastScratchTime);

      document.getElementById("scratchResult").innerText = `🎉 Scratched: +${reward} SIMA!`;
      checkScratchAvailability();
  };

  window.switchTab = function(tabId, btn) {
      document.querySelectorAll('.view').forEach(v => v.classList.remove('active'));
      document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
      document.getElementById(tabId).classList.add('active');
      btn.classList.add('active');
  };

  window.tapCoin = function(event) {
      if (!currentUsername) return;
      updateDBBalance(0.00001);

      let floatText = document.createElement('div');
      floatText.className = 'float-text';
      floatText.innerText = '+0.00001';
      let wrapper = document.getElementById('coinWrapper');
      floatText.style.left = (event.offsetX - 20) + 'px';
      floatText.style.top = (event.offsetY - 20) + 'px';
      wrapper.appendChild(floatText);
      setTimeout(() => floatText.remove(), 800);
  };

  window.spinWheel = function() {
      if ((window.simaBalance || 0) < 5) return alert("Requires 5 SIMA!");
      let won = [0, 1, 3, 5, 10, 25][Math.floor(Math.random() * 6)];
      updateDBBalance(-5 + won);
      document.getElementById("spinResult").innerText = won > 0 ? `🎉 Won: +${won} SIMA!` : `😢 Better Luck!`;
  };

  window.buyMiner = function() {
      if (minerActive) return alert("Miner already running!");
      if (window.simaBalance < 20) return alert("Requires 20 SIMA!");
      updateDBBalance(-20);
      set(ref(db, `users/${currentUsername}/miner`), true);
      startMining();
  };

  function startMining() {
      minerActive = true;
      document.getElementById("minerStatus").innerText = "⚡ Active (+0.0001 SIMA/sec)";
      document.getElementById("profMiner").innerText = "⚡ Active";
      document.getElementById("profMiner").style.color = "#2ecc71";
      setInterval(() => updateDBBalance(0.0001), 1000);
  }

  window.submitWithdraw = function() {
      let input = document.getElementById("walletInput").value.trim();
      let method = document.getElementById("method").value;
      let reqAmount = parseFloat(document.getElementById("withdrawAmount").value);

      if (!input || isNaN(reqAmount)) return alert("Please enter payment details and amount!");
      if (reqAmount < 50) return alert("Minimum withdrawal amount is 50 SIMA!");
      if ((window.simaBalance || 0) < reqAmount) return alert("Insufficient SIMA Balance!");

      // Instant Deduction & Log as Success (No Admin Approval Required)
      set(ref(db, 'withdrawals/' + Date.now()), { 
          username: currentUsername, 
          amount: reqAmount, 
          method: method, 
          address: input, 
          status: 'Instant Paid' 
      });

      updateDBBalance(-reqAmount);
      document.getElementById("withdrawAmount").value = "";
      document.getElementById("walletInput").value = "";
      alert(`🎉 Successful! ${reqAmount} SIMA deducted instantly.`);
  };

  window.logout = function() { localStorage.removeItem('sima_username'); location.reload(); };

  function updateDBBalance(amount) {
      window.simaBalance = (window.simaBalance || 0) + amount;
      updateDisplay();
      runTransaction(ref(db, 'users/' + currentUsername), (user) => {
          if (user) user.balance = (user.balance || 0) + amount;
          return user;
      });
  }

  function updateDisplay() {
      let balStr = (window.simaBalance || 0).toFixed(5);
      document.getElementById("balance").innerText = balStr;
      document.getElementById("profBalance").innerText = balStr + " SIMA";

      document.getElementById("adCountDisplay").innerText = adCount;
      document.getElementById("profAds").innerText = adCount + "/20";

      let adBtn = document.getElementById("adBtn");
      if (adBtn) adBtn.disabled = adCount >= 20;
  }
</script>

</body>
</html>

Is code me ads laga do 


// Rewarded Popup

show_11669909('pop').then(() => {
    // user watch ad till the end or close it in interstitial format
    // your code to reward user for rewarded format
}).catch(e => {
    // user get error during playing ad
    // do nothing or whatever you want
})

        

// In-App Interstitial

show_11
