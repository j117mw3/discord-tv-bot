# Discord TV Bot - User Guide

This guide explains how to use the remote control interface to manage your media broadcasts.

---

## 🚀 The Essential Workflow (Read This First!)

The Bot is a **remote control**, not a video streamer. To start a "Watch Party," you must follow these steps in order:

1.  **Launch the Bot:** Run the bot on your host computer (`python bot.py`).
2.  **Open Discord on the Host:** Log into Discord on the **same computer** that is playing VLC.
3.  **Start the Stream:** 
    *   Join a Voice Channel in your server.
    *   Click the **"Share Your Screen"** button.
    *   DO NOT Select the **VLC Media Player window**, Instead **Choose your Main Screen**.
4.  **Connect as a Viewer:** Open Discord on your phone or another device, join that same Voice Channel, and you can now use the Bot's buttons to control the show!

---

## 🎮 Control Panel Features

The bot posts a persistent control panel at the bottom of your designated TV channel.

### Panel Display Shows:
- 📺 Current show/stream name
- 🔊 Current volume percentage
- ▶ Playback status (Playing/Paused)
- 📊 Episode number (e.g., "2 of 24")
- 🔀 Shuffle mode (Normal/Shuffle Episodes/Random)
- 📼 Now Playing episode name
- ⏱️ Progress bar with timestamps
- ⏭️ Up Next (if queue has items)

---

## Quick Controls (Main Row)

| Button | Action |
|--------|--------|
| **⏮** | Previous Episode |
| **◀ 15s** | Seek backward 15 seconds |
| **⏸ Pause** | Toggle play/pause |
| **15s ▶** | Seek forward 15 seconds |
| **⏭** | Next Episode (or random if shuffle enabled) |

---

## Shows & Streams Menu

The dropdown menu is your command center. Use it to access:

### 📺 Browse Shows
Opens the full show library browser
- Navigate by page
- Select show → season → episode
- Shows marked with ▶ are currently playing

### 📑 TV Queue
Manage your watch queue
- **➕ Browse to Add** - Add episodes to queue
- **▶ Play Next Now** - Skip to next queued item
- **🗑 Clear Queue** - Empty the entire queue
- Queue auto-plays when episodes end (Normal mode only)

### 📡 Open Stream
Browse live streams by category
- Requires `Streams.json` configuration
- Supports M3U8 and direct video URLs
  *   **YouTube:** Paste a YouTube URL into the popup. The bot will use `yt-dlp` to resolve it and start playing immediately on the Host PC.
- Seek/skip controls disabled for streams

### 🔀 Shuffle Mode
Cycles through shuffle modes:
- **Normal** - Play episodes in order
- **Shuffle Episodes** - Random episodes from current show
- **Random** - Random show + random episode

### 🫥 Hide Panel / 🪄 Show Panel
Toggle the embed display
- Hide = buttons only (cleaner look)
- Show = full embed with details
- State persists across restarts

### 🔄 Refresh Library
Rescan the `C:\Shows` folder
- Picks up newly added shows/episodes
- Updates episode counts
- Does not interrupt playback

### 📜 Watch History
View recent playback history
- Shows last 10 entries
- Displays: show, episode, action, user, timestamp
- Click numbered buttons to replay historical entries
- Actions tracked: selected, skipped, auto-played, from queue

### 🖥️ Fullscreen Fix
Force VLC back into fullscreen
- Useful if VLC loses focus or exits fullscreen
- Brings VLC window to the foreground
- Windows-specific feature

### 🔊 Volume Up / 🔉 Volume Down
Adjust VLC volume
- Each click = ±10%
- Range: 0-100%
- Updates panel immediately

---

## Show Browser

### Navigation
1. Select a show from the dropdown (up to 25 shows per page)
2. Use **⬅ Prev** / **Next ➡** to page through shows
3. Click **💡 Suggestions** to view community requests

### Show Details
- Episode count shown next to each show
- ▶ marker indicates currently playing show

### Season Browser (if show has subfolders)
- Lists all seasons and loose episodes
- Select a season to view its episodes
- 📁 = Season folder
- 📄 = Loose episodes in root

### Episode Browser
- Shows episode list with smart parsing
- Format: `S01E01 - Episode Title`
- Up to 25 episodes per page
- ▶ marker shows currently playing episode
- Select to play immediately

---

## Queue System

### Adding to Queue
1. **Shows → Browse Shows**
2. Enable queue mode: **TV Queue → ➕ Browse to Add**
3. Navigate to the episode and select
4. Confirmation shows queue size

### Queue Behavior
- Queue only activates in **Normal** mode (not shuffle)
- Auto-plays when the current episode ends
- Can manually skip to the next queue item
- Persists across bot restarts
- Displays "Up Next" in main panel

### Queue Management
- **Play Next Now** - Skip current and load next queue item
- **Clear Queue** - Remove all queued items
- View queue size and items

---

## Watch History

### Tracked Actions
- **selected** - Manually chosen from browser
- **skipped** - Used next/prev buttons
- **auto:ended** - Auto-played when episode finished
- **auto:shuffle** - Loaded from shuffle mode
- **auto:queue** - Loaded from queue
- **restore** - Resumed on bot startup

### History Display
- Last 10 entries shown (most recent first)
- Shows: show name, episode, action type, user, timestamp
- Click numbered buttons to replay
- Full history stored in `watch_history.json` (200 max)

---

## Suggestion Box

### Requesting Shows
1. **Shows → Browse Shows → 💡 Suggestions**
2. Click **➕ Suggest a Show**
3. Enter show name in modal
4. Suggestion posted to channel with reaction voting

### Voting
- React ✅ to upvote
- React ❌ to downvote
- Anyone can vote on suggestions
- Helps prioritize what to add to library

---

## Streams

### Setup
Create `Streams.json` in bot folder:
```json
{
  "Category Name": [
    {"name": "Stream Name", "url": "https://example.com/stream.m3u8"}
  ]
}
```

### Playing Streams
1. **Shows → Open Stream**
2. Select category
3. Select stream
4. Stream loads fullscreen

### Stream Limitations
- Seek controls disabled (live content)
- Episode navigation disabled
- Pause/volume still work
- Shows "LIVE" in progress bar

---

## Shuffle Modes Explained

### Normal Mode
- Episodes play sequentially
- Next button advances to next episode
- At end of show: restarts from episode 1
- Queue system active

### Shuffle Episodes
- Picks random episodes from **current show only**
- Next button picks new random episode
- Good for rewatching favorites
- Queue disabled

### Random Mode
- Picks random show, then random episode
- Maximum variety
- Never picks same show twice in a row
- Queue disabled

---

## Panel Behavior

### Auto-Repost
Panel automatically reposts at the bottom of the channel when:
- Any message is sent in the TV channel
- A new show/episode loads
- Shuffle changes show

### Live Updates
Panel edits in place for:
- Playback status changes (play/pause)
- Progress bar updates (every 5 seconds)
- Volume changes
- Error states

### Old Panels
- Old panels automatically deleted
- Keeps channel clean
- Only one active panel at a time

---

## File Organization Best Practices

### Recommended Structure
```
C:\Shows\
├── Breaking Bad\
│   ├── Season 1\
│   │   ├── S01E01 - Pilot.mkv
│   │   ├── S01E02 - Cat's in the Bag.mkv
│   │   └── ...
│   ├── Season 2\
│   │   └── ...
└── The Sopranos\
    └── S01E01 - The Sopranos.mkv  ← Loose episodes OK
```

### Episode Naming
- **Best**: `S01E01 - Episode Title.mkv`
- **Good**: `1x01 - Episode Title.mkv`
- **OK**: `Episode 01.mkv`

---

## Common Workflows

### Binge Watching
1. Browse to show
2. Select first episode
3. Episodes auto-advance
4. Add future episodes to queue for seamless transition

### Random Entertainment
1. Set shuffle mode to "Random"
2. Hit next when you want something different
3. System avoids repeating last show

### Scheduled Watch Party
1. Pre-load queue with chosen episodes
2. Everyone sees "Up Next" in panel
3. Use "Play Next Now" to skip if needed

### Catching Up
1. Check Watch History
2. See what others have watched
3. Click numbered button to jump to that episode

---

## Tips & Tricks

### Fast Navigation
- Use page numbers to jump quickly through large libraries
- Season browser skips straight to season of interest

### Queue Pre-Loading
- Load entire season into queue for uninterrupted viewing
- Queue survives bot restarts

### Volume Safety
- Bot remembers volume across restarts
- Set once, enjoy consistent volume

### Fullscreen Issues
- If VLC exits fullscreen: use Fullscreen Fix
- Bot auto-applies fullscreen on every episode load

### Panel Cleanup
- Send any message to force panel repost to bottom
- Old panels auto-delete to keep channel tidy

---

## Troubleshooting

### Panel not updating
- Wait 5 seconds (watchdog interval)
- Try toggling pause/play

### Episode won't play
- Check file isn't corrupted (try in VLC directly)
- Check format is supported
- Use Refresh Library if recently added

### Queue not auto-playing
- Ensure shuffle mode is "Normal"
- Check queue isn't empty
- Episode must fully finish (not skipped)

### History not showing my watches
- History only tracks actions via Discord
- Direct VLC controls don't log
- Check `watch_history.json` file exists

---

## Privacy & Permissions

### What the bot sees:
- Messages in the designated TV channel only
- User display names (not real names)
- Interaction events (button clicks)

### What the bot stores:
- Watch history with display names
- Queue with display names
- Suggestions with display names
- Playback state

### What the bot needs:
- Send Messages (post panel)
- Embed Links (rich embeds)
- Attach Files (show artwork)
- Add Reactions (suggestion voting)
- Read Message History (cleanup old panels)

---

Enjoy your remote-controlled TV experience! 🍿
