<div align="center">

# 📡 WhatsApp Channel JID Finder

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=600&size=22&pause=1000&color=25D366&center=true&vCenter=true&width=600&lines=Extract+Newsletter+JIDs+from+WhatsApp+Web;Find+your+Channel+ID+in+seconds;No+external+tools+needed+on+PC!" alt="Typing SVG" />
</p>

<p align="center">
  <a href="https://github.com/yourusername/whatsapp-channel-jid-finder/stargazers"><img src="https://img.shields.io/github/stars/yourusername/whatsapp-channel-jid-finder?style=for-the-badge&logo=github&color=FFD700" alt="Stars"></a>
  <a href="https://github.com/yourusername/whatsapp-channel-jid-finder/network/members"><img src="https://img.shields.io/github/forks/yourusername/whatsapp-channel-jid-finder?style=for-the-badge&logo=github&color=00BFFF" alt="Forks"></a>
  <a href="https://github.com/yourusername/whatsapp-channel-jid-finder/issues"><img src="https://img.shields.io/github/issues/yourusername/whatsapp-channel-jid-finder?style=for-the-badge&logo=github&color=FF4500" alt="Issues"></a>
  <a href="#"><img src="https://img.shields.io/badge/License-MIT-green.svg?style=for-the-badge&color=25D366" alt="License"></a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/WhatsApp-25D366?style=for-the-badge&logo=whatsapp&logoColor=white" alt="WhatsApp">
  <img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" alt="JavaScript">
  <img src="https://img.shields.io/badge/IndexedDB-000000?style=for-the-badge&logo=indexeddb&logoColor=white" alt="IndexedDB">
  <img src="https://img.shields.io/badge/Console-Hacker?style=for-the-badge&logo=gnubash&logoColor=white&color=2E2E2E" alt="Console">
</p>

---

### ✨ A simple, browser-based method to extract newsletter JIDs from WhatsApp Web — no extensions, no downloads (on PC)!

</div>

---

## 🚀 Quick Overview

This repository provides a **single JavaScript snippet** that you can run directly in your browser's Developer Console to extract all **WhatsApp Channel Newsletter JIDs** from WhatsApp Web's IndexedDB storage.

> ⚡ **No external software required on PC** — just your browser's built-in DevTools!

---

## 📋 Prerequisites

| Platform | Requirement |
|----------|-------------|
| 💻 **PC (Windows/Linux/Mac)** | Any modern browser with Developer Tools |
| 📱 **Mobile** | External browser with DevTools support (recommended: **Devil Browser: Web Inspector**) |

---

## 🛠️ Step-by-Step Guide

### 💻 For PC Users (Windows / Linux / macOS)

> You **do not** need to install any external browser. Use your existing browser's built-in Developer Tools.


#### Step 1: Login to WhatsApp Web & Select Your Channel

1. Open [web.whatsapp.com](https://web.whatsapp.com) in your browser
2. Scan the QR code with your phone to log in
3. Click on the **Channel** you want the JID of

<p align="center">
  <img src="https://ibb.co/k6xv6Df6" alt="WhatsApp Web opening & Channel Selection" width="600">
  <br>
  <em>📸 Screenshot: WhatsApp Web with channel selected</em>
</p>

---
#### Step 2: Open Developer Tools

| OS | Shortcut |
|----|----------|
| 🪟 **Windows / Linux** | `Ctrl + Shift + I` or press `F12` |
| 🍎 **Mac** | `Cmd + Option + I` |

<p align="center">
  <img src="https://ibb.co/35x6RQ6z" alt="Open DevTools on PC" width="600">
  <br>
  <em>📸 Screenshot: Opening console tab Developer Tools in your browser</em>
</p>

---

#### Step 3: Open Console & Paste the Script

1. In DevTools, click on the **Console** tab
2. Copy and paste the script below
3. Press **Enter**

<p align="center">
  <img src="https://ibb.co/C5LSpy8n" alt="Console Tab in DevTools" width="600">
  <br>
  <em>📸 Screenshot: Getting results from Console tab in Developer Tools</em>
</p>

---

### 📱 For Mobile Users

> Mobile browsers typically don't have built-in DevTools. You'll need an external browser.

#### Step 1: Download Devil Browser

Download **"Devil Browser: Web Inspector"** from your app store:

<p align="center">
  <a href="YOUR_APP_STORE_LINK_HERE">
    <img src="https://img.shields.io/badge/Download-Devil%20Browser-25D366?style=for-the-badge&logo=android&logoColor=white" alt="Download Devil Browser">
  </a>
</p>

<p align="center">
  <img src="YOUR_SCREENSHOT_LINK_STEP_1_MOBILE_DEVIL_BROWSER" alt="Devil Browser App" width="300">
  <br>
  <em>📸 Screenshot: Devil Browser installation / interface</em>
</p>

---

#### Step 2: Login to WhatsApp Web

1. Open Devil Browser
2. Navigate to [web.whatsapp.com](https://web.whatsapp.com)
3. Log in by scanning the QR code
4. Click on your desired **Channel**

<p align="center">
  <img src="YOUR_SCREENSHOT_LINK_STEP_2_MOBILE_WHATSAPP" alt="WhatsApp Web on Mobile Browser" width="300">
  <br>
  <em>📸 Screenshot: WhatsApp Web logged in via Devil Browser</em>
</p>

---

#### Step 3: Open Dev Tools & Run Script

1. Open the **Dev Tools** option in Devil Browser
2. Make sure you're on the **Console** tab
3. Paste the script below and hit **Enter**

<p align="center">
  <img src="YOUR_SCREENSHOT_LINK_STEP_3_MOBILE_CONSOLE" alt="Dev Tools Console on Mobile" width="300">
  <br>
  <em>📸 Screenshot: Console open in Devil Browser</em>
</p>

---

## 🔥 The Script

Copy and paste this entire block into your browser console:

```javascript
(async () => {
  const dbs = await window.indexedDB.databases();
  const channels = new Map();

  for (const dbInfo of dbs) {
    if (!dbInfo.name) continue;

    const db = await new Promise(res => {
      const req = indexedDB.open(dbInfo.name);
      req.onsuccess = () => res(req.result);
      req.onerror = () => res(null);
    });

    if (!db) continue;

    for (const storeName of Array.from(db.objectStoreNames)) {
      try {
        const tx = db.transaction(storeName, 'readonly');
        const store = tx.objectStore(storeName);
        const records = await new Promise(res => {
          const req = store.getAll();
          req.onsuccess = () => res(req.result);
          req.onerror = () => res([]);
        });

        records.forEach(item => {
          if (!item) return;
          const str = JSON.stringify(item);
          const jidMatch = str.match(/\d{15,20}@newsletter/);
          if (jidMatch) {
            const jid = jidMatch[0];
            const name = item.name || item.subject || item.title || (str.includes("PUT_YOUR_WHATSAPP_CHANNEL_NAME_HERE") ? "PUT_YOUR_WHATSAPP_CHANNEL_NAME_HERE" : "Unknown");
            if (!channels.has(jid) || channels.get(jid) === "Unknown") {
              channels.set(jid, name);
            }
          }
        });
      } catch(e) {}
    }
  }

  console.log("%c--- CHANNEL LIST ---", "color: #00e676; font-weight: bold; font-size: 14px;");
  channels.forEach((name, jid) => {
    if (name.toLowerCase().includes("mehtab") || name === "PUT_YOUR_WHATSAPP_CHANNEL_NAME_HERE") {
      console.log(`%c👉 ${name}: ${jid} (YOUR CHANNEL)`, "color: #00ff00; font-weight: bold; font-size: 15px;");
    } else {
      console.log(`${name}: ${jid}`);
    }
  });
})();
```

---

## ✅ Expected Output

After running the script, you'll see a beautifully formatted list in your console:

```
--- CHANNEL LIST ---
My Awesome Channel: 123456789012345@newsletter
👉 Mehtab's Channel: 987654321098765@newsletter (YOUR CHANNEL)
Tech Updates: 112233445566778@newsletter
```

<p align="center">
  <img src="YOUR_SCREENSHOT_LINK_EXPECTED_OUTPUT" alt="Expected Console Output" width="600">
  <br>
  <em>📸 Screenshot: Console output showing extracted JIDs</em>
</p>

---

## ⚙️ Customization

Want to highlight your own channel? Replace this line in the script:

```javascript
name === "PUT_YOUR_WHATSAPP_CHANNEL_NAME_HERE"
```

With your actual channel name:

```javascript
name === "Your Channel Name"
```

Or add your name to the highlight filter:

```javascript
name.toLowerCase().includes("yourname")
```

---

## 🛡️ Safety & Privacy

- ✅ This script runs **entirely in your browser** — no data is sent anywhere
- ✅ It only **reads** from IndexedDB — nothing is modified or deleted
- ✅ No external dependencies or libraries required
- ✅ Fully open-source and transparent

---

## 🐛 Troubleshooting

| Issue | Solution |
|-------|----------|
| Script returns empty | Make sure you're logged in and have opened a channel |
| `indexedDB` not found | Ensure you're on WhatsApp Web, not WhatsApp Desktop app |
| Mobile browser crashes | Try clearing cache or use a different DevTools browser |
| JID not showing | Some channels may not be cached yet — try scrolling through the channel list first |

---

## 🤝 Contributing

Contributions are welcome! Feel free to:

- 🐛 Report bugs via [Issues](../../issues)
- 💡 Suggest new features
- 🔧 Submit pull requests

---

## 📜 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

<div align="center">

### Made with 💚 for the WhatsApp Community

<p align="center">
  <img src="https://komarev.com/ghpvc/?username=yourusername&label=Repository%20Views&color=25D366&style=flat-square" alt="Profile Views">
</p>

**⭐ Star this repo if it helped you!**

</div>
