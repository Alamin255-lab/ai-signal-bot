# ai-signal-bot
RSI EMA AI Signal Demo Bot

<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>AI Signal Bot</title>
<style>
body {
  margin: 0;
  padding: 20px;
  background: #071421;
  color: white;
  font-family: Arial, sans-serif;
}
.card {
  max-width: 480px;
  margin: auto;
  padding: 20px;
  background: #102638;
  border-radius: 16px;
}
h2 { text-align: center; color: #5eead4; }
.info {
  padding: 14px;
  margin: 12px 0;
  border-radius: 10px;
  background: #19374b;
}
button {
  width: 100%;
  padding: 14px;
  margin-top: 10px;
  border: 0;
  border-radius: 9px;
  background: #14b8a6;
  color: #041b25;
  font-size: 16px;
  font-weight: bold;
}
.small { color: #b8c9d6; font-size: 13px; }
</style>
</head>
<body>
<div class="card">
  <h2>🍏 AI Signal Bot</h2>
  <p class="small">শিক্ষামূলক Forex Demo • ভার্চুয়াল টাকা</p>

  <div class="info">RSI: <b id="rsi">50</b></div>
  <div class="info">EMA: <b id="ema">100.00</b></div>
  <div class="info">Signal: <b id="signal">WAIT</b></div>
  <div class="info">Demo Balance: ৳<b id="balance">10000</b></div>
  <div class="info">Demo Position: <b id="position">None</b></div>

  <button onclick="scan()">নতুন ডেমো সিগন্যাল</button>
  <button onclick="trade()">ভার্চুয়াল ট্রেড খুলুন</button>
  <button onclick="closeTrade()">ভার্চুয়াল ট্রেড বন্ধ করুন</button>

  <p id="message" class="small">
    শুরু করতে নতুন ডেমো সিগন্যাল চাপুন।
  </p>
  <p class="small">
    সতর্কতা: এটি বাস্তব বাজারের ডেটা নয়। সিগন্যাল লাভের নিশ্চয়তা দেয় না।
  </p>
</div>
<script>
let balance = 10000;
let position = null;
let entry = 0;
let price = 100;
let signal = "WAIT";

function scan() {
  price += (Math.random() - 0.5) * 2;
  const rsi = Math.floor(20 + Math.random() * 60);
  const ema = price + (Math.random() - 0.5) * 2;

  signal = rsi < 35 && price > ema ? "BUY" :
           rsi > 65 && price < ema ? "SELL" : "WAIT";

  document.getElementById("rsi").textContent = rsi;
  document.getElementById("ema").textContent = ema.toFixed(2);
  document.getElementById("signal").textContent = signal;
  document.getElementById("message").textContent =
    "শুধু অনুশীলনের জন্য তৈরি নমুনা সিগন্যাল।";
}

function trade() {
  if (position) {
    document.getElementById("message").textContent =
      "আগে খোলা ভার্চুয়াল ট্রেড বন্ধ করুন।";
    return;
  }
  if (signal === "WAIT") {
    document.getElementById("message").textContent =
      "সিগন্যাল WAIT। আগে নতুন ডেমো সিগন্যাল নিন।";
    return;
  }
  position = signal;
  entry = price;
  document.getElementById("position").textContent =
    position + " @ " + entry.toFixed(2);
  document.getElementById("message").textContent =
    "ভার্চুয়াল ট্রেড খোলা হয়েছে।";
}

function closeTrade() {
  if (!position) {
    document.getElementById("message").textContent =
      "বন্ধ করার মতো কোনো ভার্চুয়াল ট্রেড নেই।";
    return;
  }
  price += (Math.random() - 0.5) * 2;
  const pnl = position === "BUY" ? price - entry : entry - price;
  balance += pnl * 100;
  document.getElementById("balance").textContent =
    balance.toFixed(2);
  document.getElementById("position").textContent = "None";
  document.getElementById("message").textContent =
    "ভার্চুয়াল ফলাফল: " + (pnl * 100).toFixed(2);
  position = null;
}

</script>
</body>
</html>
