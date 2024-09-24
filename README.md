---

<div align="center">
<img src="https://i.imgur.com/MkFud1l.png" align="center" alt="Logo" height="100">
<br>
<br>
<strong><i>Bot Discord untuk mengetahui detail server SAMP tertentu + Penggunaan Fitur Chatbot (OpenAI) </i></strong>
<br>
<br>
</div>
<hr>
<br>

## CMD List Bot Discord RZ 📍
- Bot ini dapat menanyakan status server SA-MP dan menampilkan jumlah pemain. (/players)<br />
- Perintah untuk membalas dengan alamat IP server.<br />
- Fitur aplikasi bot di DM. (/apply) [Fitur ini akan disempurnakan di versi mendatang]<br />
- Dapat mencari informasi tentang ban (/sban) dengan implementasi SQL yang bisa diedit.<br />
- Dapat mencabut ban (/unbanban) dengan implementasi SQL yang bisa diedit.<br />
- Fitur pencatatan untuk laporan, dengan implementasi SQL yang bisa diedit.<br />
- Pemroses perintah yang memungkinkan Anda mengubah karakter perintah bot.<br />
- Perintah utilitas /clear untuk menghapus pesan dalam jumlah banyak.<br />
- Mendukung perubahan konfigurasi secara langsung.

---

## Setup Awal 📝
- Anda dapat langsung menerapkan bot ini menggunakan Dyno gratis yang ditawarkan oleh Heroku. Cukup daftar akun gratis di Heroku dan klik tombol Deploy di bawah.<br />
- Untuk tutorial lengkap, [klik di sini]((https://www.youtube.com/@RandyKurniawan)).

---

## Deployment 📝
[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

---

## Menambahkan Fitur Chatbot 🤖
Untuk menambahkan fitur chatbot ke dalam bot Discord ini, ikuti langkah-langkah berikut:

### 1. Install Dependensi yang Dibutuhkan
Pertama, Anda perlu menginstall library `openai` untuk memanfaatkan API Chatbot. Jalankan perintah berikut untuk menambahkannya ke dalam proyek Anda:
```bash
npm install openai dotenv
```

### 2. Konfigurasi OpenAI API
Buat file `.env` di direktori proyek dan tambahkan API Key dari OpenAI:
```
OPENAI_API_KEY=your-openai-api-key-here
```

### 3. Modifikasi Kode Bot
Tambahkan kode berikut ke dalam file utama bot (`index.js`) untuk menangani pesan yang dikirimkan ke chatbot:

```javascript
const { Client, GatewayIntentBits } = require('discord.js');
const openai = require('openai');
require('dotenv').config();

openai.apiKey = process.env.OPENAI_API_KEY;

const client = new Client({
    intents: [
        GatewayIntentBits.Guilds,
        GatewayIntentBits.GuildMessages,
        GatewayIntentBits.MessageContent
    ]
});

client.on('messageCreate', async message => {
    // Cegah bot membalas pesannya sendiri
    if (message.author.bot) return;

    // Perintah untuk memulai chatbot
    if (message.content.startsWith('!chatbot')) {
        const userMessage = message.content.replace('!chatbot ', '');
        const response = await openai.createCompletion({
            model: 'text-davinci-003',
            prompt: userMessage,
            max_tokens: 150
        });

        message.channel.send(response.data.choices[0].text.trim());
    }
});

client.login('YOUR_DISCORD_TOKEN');
```

### 4. Jalankan Bot
Setelah menambahkan kode di atas, Anda dapat menjalankan bot menggunakan Node.js:
```bash
node index.js
```

Sekarang, Anda bisa menggunakan fitur chatbot di Discord dengan mengetik:
```
!chatbot [pesan Anda]
```

### 5. Commit dan Push
Jangan lupa untuk menyimpan perubahan Anda ke GitHub dengan melakukan commit dan push:
```bash
git add .
git commit -m "Menambahkan fitur chatbot"
git push origin main
```

---

