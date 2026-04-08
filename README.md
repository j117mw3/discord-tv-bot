# Discord TV Remote Bot 📺

A powerful remote-control system that transforms any computer with VLC Media Player into a Discord-accessible streaming hub. 

> **⚠️ IMPORTANT CONCEPT:** This bot does **not** stream video directly through Discord's servers. It controls a local instance of VLC on your **Host PC**. To let others watch, you must manually start a "Screen Share" in a Discord Voice Channel from the same computer running the bot.

---

## 🌟 Core Concept: The Two-Part Setup

To use this project, you are managing two separate things:

1.  **The Host (The TV):** A PC/Server running the Bot, VLC Media Player, and an active Discord Screen Share in a Voice Channel.
2.  **The Controller (The Remote):** Any device (Phone, Tablet, Second Monitor) where you join the same Discord server to interact with the Bot's buttons and menus.

---

## ✨ Features

*   🎬 **Show Browser** – Navigate your local library with pagination and season support.
*   📑 **Watch Queue** – Add episodes to a queue; the bot auto-plays them when the current one ends.
*   📡 **Live & YouTube Streams** – Paste a YouTube link or M3U8 URL via Discord, and the Host PC will instantly begin playing it.
*   🔄 **On-the-Fly Streaming** – Use `Streams.json` to manage permanent live stream categories (News, Lofi, etc.).
*   📜 **Watch History** – Track what has been played, by whom, and when.
*   💡 **Suggestion Box** – Let your community vote on which shows you should add to the library next.
*   🎮 **Full Remote Control** – Play/Pause, Seek (15s), Volume, Skip, and Shuffle modes—all via Discord buttons.
*   🖥️ **Fullscreen Management** – One-click "Fullscreen Fix" to force VLC back to the front of your screen.

---

## 🛠️ Prerequisites

*   **A 24/7 Device:** A PC, Raspberry Pi, or Cloud VM that stays on.
*   **VLC Media Player (64-bit):** Must be installed on the Host PC.
*   **Python 3.9+** and **yt-dlp** (for YouTube support).
*   **Discord Bot Token:** Created via the [Discord Developer Portal](https://discord.com/developers/applications).

---

## 🚀 Quick Start

1.  **Setup the Bot:** Follow the [Installation Guide](Installation.md).
2.  **Prepare your Media:** Organize shows in `C:\Shows` (Windows) or your configured path.
3.  **Start the Broadcast:**
    *   Open Discord on the **Host PC**.
    *   Enter a Voice Channel and click **"Share Your Screen"** $\rightarrow$ Select Share Screen.
    *   Run `python bot.py`.
    
5.  **Control:** Join the server from your phone or another device and use the Control Panel!

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
