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
---

# RZ Discord Bot with AI Integration

## Deskripsi Projek
Proyek ini adalah sebuah bot Discord yang terintegrasi dengan Kecerdasan Buatan (AI) menggunakan API dari OpenAI. Bot ini dapat melakukan percakapan secara dinamis dengan pengguna, menjawab pertanyaan, dan memproses perintah khusus terkait server SA-MP (San Andreas Multiplayer). Bot ini dirancang untuk komunitas SA-MP, dengan kemampuan untuk menampilkan informasi tentang server dan memberikan fitur interaktif melalui AI chatbot.

---

## Fitur Utama 📍
- **Menampilkan Status Server**: Mengambil dan menampilkan informasi tentang status server SA-MP, termasuk jumlah pemain yang sedang online.
- **Respon AI**: Bot dapat merespons pesan pengguna menggunakan teknologi pemrosesan bahasa alami (Natural Language Processing) dari OpenAI, melalui perintah `!chatbot [pesan]`.
- **Perintah Utilitas**: Termasuk perintah untuk menghapus pesan dalam jumlah besar (`/clear`) dan mengubah konfigurasi bot secara langsung.
- **Pencarian Informasi Ban**: Memungkinkan pencarian informasi ban menggunakan perintah SQL yang dapat diedit.

---

## Cara Install 📝

### 1. Clone Repository
Pertama, clone repository dari GitHub ke dalam komputer Anda:
```bash
git clone https://github.com/username/discord-bot-ai
cd discord-bot-ai
```

### 2. Install Dependensi
Install semua dependensi yang diperlukan, termasuk library untuk Discord.js dan OpenAI:
```bash
npm install
npm install openai dotenv
```

### 3. Konfigurasi API
Buat file `.env` di root directory dan tambahkan API Key dari OpenAI:
```
DISCORD_TOKEN=your-discord-token-here
OPENAI_API_KEY=your-openai-api-key-here
```

### 4. Menjalankan Bot
Setelah semua konfigurasi selesai, jalankan bot dengan perintah berikut:
```bash
node bot.js
```

---

## Contoh Penggunaan

- Ketik `!chatbot [pesan]` di channel Discord untuk mendapatkan respon dari AI.
- Ketik `/players` untuk menampilkan jumlah pemain yang sedang online di server SA-MP.
- Ketik `/clear [jumlah pesan]` untuk menghapus sejumlah pesan dari channel secara instan.

---

## Screenshot Akun GitHub
![GitHub Profile Screenshot](./images/github-profile.png)

---

## Screenshot Proyek
![Proyek Screenshot](./images/project-screenshot.png)

---

## Integrasi AI

Proyek ini menggunakan model kecerdasan buatan (AI) dari OpenAI yang berfungsi untuk melakukan percakapan dengan pengguna secara interaktif. Dengan menggunakan perintah `!chatbot`, bot dapat memproses pesan dan memberikan balasan yang sesuai berdasarkan konteks percakapan.

### Contoh Kode Integrasi AI:

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
    if (message.author.bot) return;

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

client.login(process.env.DISCORD_TOKEN);
```

---

## Link Repository GitHub
Untuk informasi lebih lanjut dan pengembangan lebih lanjut, Anda dapat mengunjungi repository GitHub proyek ini:
[Link ke Repository]([https://github.com/randkurn/rz-discord-bot])

---

