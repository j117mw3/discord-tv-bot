# Discord TV Remote Bot 📺

A powerful Discord bot that transforms VLC Media Player into a remote‑controlled streaming hub. Browse your media library, manage watch queues, and control playback—all from Discord.

> **⚠️ Important** – This bot must run on a device that stays **on 24/7** (e.g., a mini PC, an old laptop, a Raspberry Pi, or a cloud VM). It does **not** stream your personal Discord screen; instead, it runs VLC directly on that device and lets you remote‑control it via Discord.

---

## Features

- 🎬 **Show Browser** – Navigate your entire TV show library with pagination  
- 📑 **Watch Queue** – Queue up episodes and let them auto‑play  
- 🔀 **Shuffle Modes** – Random episodes or random shows  
- 📡 **Live Streams** – Support for M3U8 and other streaming formats  
- 📜 **Watch History** – Track what you’ve watched with timestamps  
- 💡 **Suggestion Box** – Community voting on new shows to add  
- 🎮 **Full Remote Control** – Play, pause, seek, skip, volume control  
- 🖥️ **Fullscreen Management** – Auto‑fullscreen with focus fixes  

---

## What You Need

### 1. A device that runs 24/7  
The bot must always be online to respond to commands. Good options:  
- A mini PC (e.g., Intel NUC, Beelink)  
- An old laptop or desktop you leave on  
- A Raspberry Pi 4/5  
- A cloud VM (AWS EC2, Google Cloud, DigitalOcean, etc.)  

### 2. Two Discord accounts  
- **Your personal Discord account** – the one you use to send commands.  
- **A separate bot account** – created at the [Discord Developer Portal](https://discord.com/developers/applications). This account will run the bot and appear in your server.  

> The bot itself **cannot** stream your screen. It runs VLC on the 24/7 device and plays media locally. You use Discord buttons to control playback remotely.

### 3. Media files or streams  
- TV shows stored on the 24/7 device (or a network drive it can access).  
- (Optional) Live stream URLs in a `Streams.json` file.

---

## Quick Start

### Prerequisites (on your 24/7 device)
- Windows or Linux  
- Python 3.9+  
- VLC Media Player  
- Discord Bot Token (from Developer Portal)

### Step‑by‑Step

1. **Clone or download this repository**  
2. **Install dependencies** – see the [full installation guide](https://github.com/j117mw3/discord-tv-bot/blob/main/Installation.md)  
3. **Set your bot token** – as environment variable `TV_BOT_TOKEN`  
4. **Edit `core.py`** – add your Discord channel ID and server ID  
5. **Create your shows folder** (e.g., `C:\Shows` or `~/Shows`)  
6. **Run the bot** – `python bot.py`

---

## Documentation

| File | Description |
|------|-------------|
| [**Installation.md**](https://github.com/j117mw3/discord-tv-bot/blob/main/Installation.md) | Complete step‑by‑step install for Windows & Linux, including environment variables, Discord bot setup, and running as a service |
| [**UserGuide.md**](https://github.com/j117mw3/discord-tv-bot/blob/main/UserGuide.md) | Full user manual – all buttons, queue, shuffle modes, watch history, and tips |
| [**Requirements.txt**](./Requirements.txt) | Python dependencies (install with `pip install -r requirements.txt`) |
| [**LICENSE**](./LICENSE) | MIT License – free to use, but credit must be given |

---

## Basic Usage (once the bot is running)

The bot posts a persistent control panel in your Discord channel:

- **⏮ / ⏭** – Previous/Next episode  
- **◀ 15s / 15s ▶** – Seek backward/forward  
- **⏸ Pause** – Toggle play/pause  
- **Shows & Streams** – Dropdown menu to browse shows, manage queue, change shuffle mode, etc.

For detailed instructions, read the [**USER_GUIDE.md**](./UserGuide.md).

---

## Folder Structure Example
```
C:\Shows\ (or ~/Shows on Linux)
├── Breaking Bad
│ ├── Season 1
│ │ ├── S01E01 - Pilot.mkv
│ │ └── S01E02 - Cat's in the Bag.mkv
│ └── Season 2
└── The Sopranos
└── S01E01 - The Sopranos.mkv
```

Supported formats: `.mp4`, `.mkv`, `.avi`, `.mov`, `.m4v`, `.wmv`, `.flv`, `.webm`

---

## Troubleshooting Quick Fixes

| Problem | Likely solution |
|---------|----------------|
| Bot doesn’t respond | Enable **MESSAGE CONTENT INTENT** in Discord Developer Portal |
| VLC errors | Install 64‑bit VLC if using 64‑bit Python |
| “BOT_TOKEN is empty” | Set `TV_BOT_TOKEN` environment variable and restart terminal |
| Fullscreen not working | Use the “Fullscreen Fix” in the Shows menu |

See [INSTALLATION.md](./Installation.md) for detailed troubleshooting.

---

## Platform Support

- ✅ **Windows 10/11** – Fully tested  
- ⚠️ **Linux** – Supported (path modifications needed – see INSTALLATION.md)  
- ❌ **macOS** – Untested (but may work with minor changes)

---

## License

This project is licensed under the **MIT License** – you are free to use, modify, and distribute it, as long as you give credit to the original author.  
See the [LICENSE](./LICENSE) file for details.

---

**Enjoy your remote‑controlled TV experience!** 🍿  
For issues or questions, open an issue on GitHub.
