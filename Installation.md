# Discord TV Bot - Installation Guide

A Discord bot that controls VLC media player remotely, allowing you to browse and play shows, streams, and manage a watch queue.

---

## Windows Installation

### 1. Install Python (3.9 or higher)

1. Download Python from [python.org](https://www.python.org/downloads/)
2. **Important**: Check "Add Python to PATH" during installation
3. Verify installation by opening Command Prompt and running:
   ```cmd
   python --version
   ```

### 2. Install VLC Media Player

1. Download VLC from [videolan.org](https://www.videolan.org/vlc/)
2. Install using the default settings
3. **Important**: Install the 64-bit version if you have 64-bit Python

### 3. Install Deno (for YouTube/streaming support)

Open PowerShell as Administrator and run:
```powershell
irm https://deno.land/install.ps1 | iex
```

Close and reopen PowerShell after installation.

### 4. Install yt-dlp (YouTube downloader)

Open Command Prompt or PowerShell and run:
```cmd
python -m pip install -U "yt-dlp[default]"
```
Depending on what browser you have, run the following:
```cmd
py -3.11 -m yt_dlp --cookies-from-browser edge --cookies cookies.txt

py -3.11 -m yt_dlp --cookies-from-browser chrome --cookies cookies.txt
```

### 5. Install Python Dependencies

Navigate to your bot folder and run:
```cmd
pip install discord.py python-vlc
```

Or if you have a `requirements.txt` file:
```cmd
pip install -r requirements.txt
```

### 6. Set Up Environment Variable (Bot Token)

#### Option A: Using System Environment Variables (Recommended)
1. Press `Win + X` and select "System"
2. Click "Advanced system settings"
3. Click "Environment Variables"
4. Under "User variables", click "New"
5. Variable name: `TV_BOT_TOKEN`
6. Variable value: `your_discord_bot_token_here`
7. Click OK and restart any open Command Prompts

#### Option B: Using PowerShell (Session-based)
```powershell
$env:TV_BOT_TOKEN = "your_discord_bot_token_here"
```
Note: This only lasts for the current PowerShell session.

#### Option C: Using Command Prompt (Session-based)
```cmd
set TV_BOT_TOKEN=your_discord_bot_token_here
```
Note: This only lasts for the current Command Prompt session.

#### Option D: Create a .env file (Alternative)
Create a file named `.env` in your bot folder:
```
TV_BOT_TOKEN=your_discord_bot_token_here
```

Then install python-dotenv:
```cmd
pip install python-dotenv
```

And add this to the top of `bot.py`:
```python
from dotenv import load_dotenv
load_dotenv()
```

### 7. Create Required Folders

Create the TV shows folder:
```cmd
mkdir C:\Shows
```

### 8. Create Configuration Files

Create a `Streams.json` file in your bot folder (optional, for live streams):
```json
{
  "News": [
    {"name": "Example Stream", "url": "https://example.com/stream.m3u8"}
  ],
  "Music": [
    {"name": "Lofi Radio", "url": "https://example.com/lofi.m3u8"}
  ]
}
```

---

## Linux Installation

### 1. Install Python (3.9 or higher)

#### Ubuntu/Debian:
```bash
sudo apt update
sudo apt install python3 python3-pip python3-venv
```

#### Fedora:
```bash
sudo dnf install python3 python3-pip
```

#### Arch:
```bash
sudo pacman -S python python-pip
```

Verify installation:
```bash
python3 --version
```

### 2. Install VLC Media Player

#### Ubuntu/Debian:
```bash
sudo apt install vlc
```

#### Fedora:
```bash
sudo dnf install vlc
```

#### Arch:
```bash
sudo pacman -S vlc
```

### 3. Install Deno

```bash
curl -fsSL https://deno.land/install.sh | sh
```

Add Deno to your PATH by adding this to your `~/.bashrc` or `~/.zshrc`:
```bash
export DENO_INSTALL="$HOME/.deno"
export PATH="$DENO_INSTALL/bin:$PATH"
```

Then reload your shell:
```bash
source ~/.bashrc  # or source ~/.zshrc
```

### 4. Install yt-dlp

```bash
python3 -m pip install -U "yt-dlp[default]"
```

### 5. Install Python Dependencies

Create a virtual environment (recommended):
```bash
python3 -m venv venv
source venv/bin/activate
```

Install dependencies:
```bash
pip install discord.py python-vlc
```

### 6. Set Up Environment Variable (Bot Token)

Add to your `~/.bashrc` or `~/.zshrc`:
```bash
export TV_BOT_TOKEN="your_discord_bot_token_here"
```

Reload your shell:
```bash
source ~/.bashrc  # or source ~/.zshrc
```

### 7. Create Required Folders

**Note**: The bot is currently hardcoded to use `C:\Shows` (Windows path). You'll need to modify `core.py`:

```bash
mkdir -p ~/Shows
```

Then edit `core.py` and change:
```python
TV_SHOWS_PATH = r"C:\Shows"
```
to:
```python
TV_SHOWS_PATH = "/home/YOUR_USERNAME/Shows"
# Or use: TV_SHOWS_PATH = os.path.expanduser("~/Shows")
```

### 8. Create Configuration Files

Create `Streams.json` in your bot folder:
```bash
nano Streams.json
```

Paste the example JSON from the Windows section above.

---

## Discord Bot Setup

### 1. Create a Discord Application

1. Go to [Discord Developer Portal](https://discord.com/developers/applications)
2. Click "New Application"
3. Give it a name (e.g., "TV Remote Bot")
4. Click "Create"

### 2. Create a Bot User

1. In your application, click "Bot" in the left sidebar
2. Click "Add Bot" → "Yes, do it!"
3. Under "TOKEN", click "Reset Token" and copy it
4. **Save this token securely** - you'll need it for the environment variable

### 3. Configure Bot Permissions

Under "Bot" settings:
- ✅ Enable "MESSAGE CONTENT INTENT"
- ✅ Enable "SERVER MEMBERS INTENT" (optional)

### 4. Set Bot Permissions

Scroll to "OAuth2" → "URL Generator":
1. Under "SCOPES", check:
   - ✅ `bot`
   
2. Under "BOT PERMISSIONS", check:
   - ✅ Send Messages
   - ✅ Embed Links
   - ✅ Attach Files
   - ✅ Read Message History
   - ✅ Add Reactions
   - ✅ Use External Emojis

3. Copy the generated URL at the bottom
4. Paste it in your browser and invite the bot to your server

### 5. Get Your Channel ID

1. In Discord, enable Developer Mode:
   - User Settings → Advanced → Developer Mode (toggle ON)
2. Right-click the channel where you want the bot to operate
3. Click "Copy Channel ID"
4. Edit `core.py` and update:
   ```python
   TV_CHANNEL_ID = 1234567891234567891  # Replace with your channel ID
   ```

### 6. Get Your Guild (Server) ID

1. Right-click your server icon
2. Click "Copy Server ID"
3. Edit `core.py` and update:
   ```python
   GUILD_ID = 1234567891234567891  # Replace with your guild ID
   ```

---

## Configuration

### Folder Structure

```
your-bot-folder/
├── bot.py
├── core.py
├── ui.py
├── Streams.json (optional)
├── tv_state.json (auto-created)
├── watch_history.json (auto-created)
├── tv_queue.json (auto-created)
└── suggestions.json (auto-created)

C:\Shows\ (or ~/Shows/ on Linux)
├── Breaking Bad/
│   ├── Season 1/
│   │   ├── S01E01 - Pilot.mkv
│   │   └── S01E02 - Cat's in the Bag.mkv
│   └── Season 2/
│       └── ...
└── The Sopranos/
    └── ...
```

### Supported Video Formats

The bot supports: `.mp4`, `.mkv`, `.avi`, `.mov`, `.m4v`, `.wmv`, `.flv`, `.webm`

---

## First Run

### Windows

1. Open Command Prompt or PowerShell
2. Navigate to your bot folder:
   ```cmd
   cd C:\path\to\your\bot
   ```
3. Run the bot:
   ```cmd
   python bot.py
   ```

### Linux

1. Open Terminal
2. Navigate to your bot folder:
   ```bash
   cd /path/to/your/bot
   ```
3. Activate virtual environment (if using):
   ```bash
   source venv/bin/activate
   ```
4. Run the bot:
   ```bash
   python3 bot.py
   ```

### Expected Output

```
2024-04-07 14:30:00  INFO      Logged in as YourBotName#1234 (123456789012345678)
2024-04-07 14:30:00  INFO      Library loaded — 15 shows, 234 total episodes
```

---

## Troubleshooting

### "Module not found" errors
```cmd
pip install discord.py python-vlc
```

### VLC not detected
- Make sure VLC is installed and in your system PATH
- On Windows, VLC should be in `C:\Program Files\VideoLAN\VLC\`
- On Linux, run `which vlc` to verify installation

### Bot doesn't respond
- Check that MESSAGE CONTENT INTENT is enabled in Discord Developer Portal
- Verify the bot has permissions in your Discord channel
- Check that `TV_CHANNEL_ID` matches your actual channel ID

### "BOT_TOKEN is empty" error
- Verify environment variable is set correctly
- Restart your terminal/command prompt after setting the variable
- Try the .env file method instead

### VLC window doesn't go fullscreen
- Use the "Fullscreen Fix" option in the Shows menu
- This is a known Windows issue with VLC window focus

---

## Running as a Service (Advanced)

### Windows (using NSSM)

1. Download NSSM from [nssm.cc](https://nssm.cc/download)
2. Install the service:
   ```cmd
   nssm install TVBot "C:\Python\python.exe" "C:\path\to\bot.py"
   nssm set TVBot AppDirectory "C:\path\to\bot"
   nssm set TVBot AppEnvironmentExtra TV_BOT_TOKEN=your_token_here
   nssm start TVBot
   ```

### Linux (using systemd)

Create `/etc/systemd/system/tvbot.service`:
```ini
[Unit]
Description=Discord TV Bot
After=network.target

[Service]
Type=simple
User=your_username
WorkingDirectory=/path/to/bot
Environment="TV_BOT_TOKEN=your_token_here"
ExecStart=/usr/bin/python3 /path/to/bot/bot.py
Restart=always

[Install]
WantedBy=multi-user.target
```

Enable and start:
```bash
sudo systemctl daemon-reload
sudo systemctl enable tvbot
sudo systemctl start tvbot
```

---

## Support

For issues or questions:
- Check the logs for error messages
- Verify all dependencies are installed
- Ensure VLC is running and accessible
- Check Discord bot permissions

---

## License

[MIT](https://github.com/j117mw3/discord-tv-bot/blob/main/LICENSE)
