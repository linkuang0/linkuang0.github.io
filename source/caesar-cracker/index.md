---
title: 凯撒密码破解工具
date: 2023-10-20
layout: post
---

<link rel="stylesheet" href="/css/caesar.css">

<div class="caesar-container">
  <h1>凯撒密码破解工具</h1>
  
  <div class="input-group">
    <textarea id="ciphertext" placeholder="请输入密文..."></textarea>
  </div>
  
  <button onclick="crackCaesar()">开始破解</button>
  
  <div id="results"></div>
</div>

<script>
function caesarDecrypt(ciphertext, shift) {
  return ciphertext.replace(/[a-zA-Z]/g, function(c) {
    const base = c < 'a' ? 65 : 97;
    return String.fromCharCode(
      (c.charCodeAt(0) - base - shift + 26) % 26 + base
    );
  });
}

function crackCaesar() {
  const ciphertext = document.getElementById('ciphertext').value;
  const resultsDiv = document.getElementById('results');
  resultsDiv.innerHTML = '';

  for (let shift = 1; shift <= 25; shift++) {
    const decrypted = caesarDecrypt(ciphertext, shift);
    const resultBox = document.createElement('div');
    resultBox.className = 'result-box';
    resultBox.innerHTML = `
      <div class="shift">Shift ${shift}:</div>
      <div class="text">${decrypted}</div>
    `;
    resultsDiv.appendChild(resultBox);
  }
}
</script>