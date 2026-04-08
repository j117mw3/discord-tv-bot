# Discord TV Remote Bot 📺

A powerful Discord bot that transforms VLC Media Player into a remote-controlled streaming hub. Browse your media library, manage watch queues, and control playback—all from Discord.

## Features

- 🎬 **Show Browser** - Navigate your entire TV show library with pagination
- 📑 **Watch Queue** - Queue up episodes and let them auto-play
- 🔀 **Shuffle Modes** - Random episodes or random shows
- 📡 **Live Streams** - Support for M3U8 and other streaming formats
- 📜 **Watch History** - Track what you've watched with timestamps
- 💡 **Suggestion Box** - Community voting on new shows to add
- 🎮 **Full Remote Control** - Play, pause, seek, skip, volume control
- 🖥️ **Fullscreen Management** - Auto-fullscreen with focus fixes

## Quick Start

### Prerequisites
- Windows or Linux PC
- Python 3.9+
- VLC Media Player
- Discord Bot Token

### Installation

1. **Clone or download this repository**

2. **Install Python dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Install additional tools:**
   ```bash
   # Deno (Windows PowerShell)
   irm https://deno.land/install.ps1 | iex
   
   # yt-dlp
   python -m pip install -U "yt-dlp[default]"
   ```

4. **Set up your bot token:**
   ```bash
   # Windows
   setx TV_BOT_TOKEN "your_discord_bot_token_here"
   
   # Linux
   export TV_BOT_TOKEN="your_discord_bot_token_here"
   ```

5. **Configure the bot:**
   - Edit `core.py` and set your `TV_CHANNEL_ID` and `GUILD_ID`
   - Create your shows folder at `C:\Shows` (Windows) or `~/Shows` (Linux)

6. **Run the bot:**
   ```bash
   python bot.py
   ```

## Usage

Once the bot is running, it will post a control panel in your designated Discord channel:

### Main Controls
- **⏮ / ⏭** - Previous/Next episode
- **◀ 15s / 15s ▶** - Seek backward/forward
- **⏸ Pause** - Toggle play/pause
- **Shows & Streams** - Access all features via dropdown menu

### Browse Shows
1. Click the "Shows & Streams" dropdown
2. Select "Browse Shows"
3. Navigate through your library
4. Select a show, then an episode to play

### Queue Management
1. Open "TV Queue" from the dropdown
2. Browse shows to add episodes
3. Queue auto-plays when current episode ends

### Shuffle Modes
- **Normal** - Play episodes sequentially
- **Shuffle Episodes** - Random episodes from current show
- **Random** - Random show + random episode

## Configuration

### Supported Video Formats
`.mp4`, `.mkv`, `.avi`, `.mov`, `.m4v`, `.wmv`, `.flv`, `.webm`

### Folder Structure
```
C:\Shows\
├── Breaking Bad\
│   ├── Season 1\
│   │   ├── S01E01 - Pilot.mkv
│   │   └── S01E02 - Cat's in the Bag.mkv
│   └── Season 2\
└── The Sopranos\
    └── ...
```

### Optional: Streams Configuration
Create `Streams.json` in the bot folder:
```json
{
  "News": [
    {"name": "Example Stream", "url": "https://example.com/stream.m3u8"}
  ]
}
```

## Files Created by Bot

- `tv_state.json` - Current playback state (position, volume, etc.)
- `watch_history.json` - History of watched episodes
- `tv_queue.json` - Persistent watch queue
- `suggestions.json` - Community show suggestions

## Discord Setup

1. Create a bot at [Discord Developer Portal](https://discord.com/developers/applications)
2. Enable **MESSAGE CONTENT INTENT**
3. Grant permissions: Send Messages, Embed Links, Attach Files, Add Reactions
4. Invite to your server
5. Copy Channel ID and Guild ID to `core.py`

## Troubleshooting

### Bot doesn't respond
- Check MESSAGE CONTENT INTENT is enabled
- Verify `TV_CHANNEL_ID` matches your channel
- Ensure bot has proper permissions

### VLC errors
- Install VLC 64-bit if using Python 64-bit
- Check VLC is in system PATH
- Try the "Fullscreen Fix" in the Shows menu

## Requirements

### Core Dependencies
- Python 3.9+
- discord.py
- python-vlc
- VLC Media Player
- yt-dlp (YouTube/stream support)
  
### Optional Tools
- Deno (for advanced streaming)

## Platform Support

- ✅ **Windows 10/11** - Fully tested
- ⚠️ **Linux** - Supported with path modifications (see INSTALLATION.md)
- ❌ **macOS** - Untested

## Contributing

Issues and pull requests are welcome!

## License

MIT License

---

**Note**: This bot is designed for personal/private use. Respect copyright laws when using media files.
