---
title: 测试加密
date: 2026-09-20
filename: 2026-09-20-test-encrypt
category: 测试
tags:
share: true
private: "true"
---
<div id="private-test">
  <p>这是一篇加密文章，输入密码后解密。</p>

  <input
    id="password"
    type="password"
    placeholder="输入密码"
    autocomplete="off"
  >

  <button id="decrypt">解密</button>

  <p id="status"></p>

  <pre id="result"></pre>
</div>

<script>
const ciphertext = `100000:db7f024eb9118ec5c6609535e55db059:ce9ea734d0ef6200dba2a540:11e3b9cac4297f4351a59e13043bef0b5160843313cc95f4270efe1bae7070258ac775e64929f3ffc499302aa0f0cd7ca1ccf61842352c0a948a8cf848c2a699c12dc39301f1070b2bb84ea5d932b76526c96daa0de941ac6c24b38d4f79d2a5b1dfcfaeb3e992f84e3333f31b2c32977f3755e0062d92e550881b92f5dc690a1317a9905eb5e57db1d72c7228cd7809e79b810e2a8d4e29cd32d4fc9d37fb158d9f78f9786f11127781518ae7a56c156a9b20623dc418632c9a6257ee9276d1d2685a0731a6280cb562e839e674a01ed58f1a1cfb6a1a6a506440fce962513476d206a62fd8f62a1efee5c29414d40f997a5a9c076d134904e05ab10ec975096ca44ecc0f45d4ae4c486e31af95eb81a6a6da3dbb5db334121c363766c000bfda786d819cf1287ce68ef6a2de413aa943cdc05b6a5e37fb63af4be206720c97cb662ec506875e528900b131ac5a72d3fe6102ee17cf87f9ec581546b176f5b7e29771dfeeccd91f73b7742917e67c963846edea1d93b83edd2fe05b8ee1b4ad9c5ffe2f071f493e9d4a73ff075175f9c8a4a87d681933465d7b643d6880f7ace01e0efce25a93d71e45362b15f490d9fe45322d9891948195df9655c2eb7b8760fc9a738d2e8fba90d67aa05d7a6a60c7a9dfbf614b4e3c00f67f35a6f13789071c762deb6da873ea`;

function hexToBytes(hex) {
  const bytes = new Uint8Array(hex.length / 2);

  for (let i = 0; i < bytes.length; i++) {
    bytes[i] = parseInt(hex.substr(i * 2, 2), 16);
  }

  return bytes;
}

async function decrypt(ciphertext, password) {
  const parts = ciphertext.split(":");

  if (parts.length !== 4) {
    throw new Error("密文格式不正确");
  }

  const iterations = parseInt(parts[0], 10);
  const salt = hexToBytes(parts[1]);
  const iv = hexToBytes(parts[2]);
  const encrypted = hexToBytes(parts[3]);

  const keyMaterial = await crypto.subtle.importKey(
    "raw",
    new TextEncoder().encode(password),
    "PBKDF2",
    false,
    ["deriveKey"]
  );

  const key = await crypto.subtle.deriveKey(
    {
      name: "PBKDF2",
      salt: salt,
      iterations: iterations,
      hash: "SHA-256"
    },
    keyMaterial,
    {
      name: "AES-GCM",
      length: 256
    },
    false,
    ["decrypt"]
  );

  const decrypted = await crypto.subtle.decrypt(
    {
      name: "AES-GCM",
      iv: iv
    },
    key,
    encrypted
  );

  return new TextDecoder().decode(decrypted);
}

document.getElementById("decrypt").addEventListener("click", async () => {
  const password = document.getElementById("password").value;
  const status = document.getElementById("status");
  const result = document.getElementById("result");

  status.textContent = "正在解密……";
  result.textContent = "";

  try {
    const text = await decrypt(ciphertext, password);

    status.textContent = "解密成功";
    result.textContent = text;
  } catch (error) {
    status.textContent = "解密失败：密码错误或密文损坏";
    console.error(error);
  }
});
</script>