# WIM (WoW Instant Messenger) - TurtleWoW Fork

A modified version of WIM optimized for TurtleWoW private server with cross-faction whisper support and Game Master detection.

## Features

### TurtleWoW Compatibility
- **30-second WHO cooldown** - Respects TurtleWoW's WHO rate limit (vs 5s retail)
- **Cross-faction whispers** - Messages display immediately, WHO info loads asynchronously
- **Removed "Block Low Level" option** - Incompatible with cross-faction system

### Game Master Support
- **GM Detection** - Detects GM flag from server (`arg6 == "GM"`) - cannot be faked by players
- **GM Icon** - Displays custom Blizzard icon instead of class icon for GMs
- **GM Title** - Shows `<GM>` prefix in window title and message names
- **"Game Master" Label** - Displays "Game Master" instead of level/race/class
- **WHO Bypass for GMs** - GMs skip the 30s WHO cooldown
- **History Support** - GM status is saved in chat history

### Performance & Reliability
- **Async WHO System** - Messages appear instantly, player info loads in background
- **Queue System** - Round-robin WHO requests with max 5 retries per player
- **Timeout Handling** - 10s timeout for normal players, 2s for GMs
- **No WHO Window Popup** - WHO requests don't open the Friends/Who frame

### Debug Mode
- `/wimdebug` - Toggle debug messages for troubleshooting
- Shows WHO queue status, cache status, GM detection, and timing info

## Installation

1. Extract to `Interface/AddOns/WIM/`
2. (Optional) Add custom `Blizzard.tga` (64x64) to `Interface/AddOns/WIM/Images/` for GM icon
3. Reload UI or restart WoW

## Commands

| Command | Description |
|---------|-------------|
| `/wim` | Open WIM options |
| `/wimdebug` | Toggle debug mode |
| `/wim history` | Open history window |
| `/wim clear history` | Clear all history |

## Files Modified

### WIM.lua
- Added `WIM_IsGM` variable and GM spell check ("Teleport to GM Island")
- Added `WIM_Debug` system with `/wimdebug` command
- Modified `WIM_Update()` - 30s cooldown for players, bypass for GMs
- Modified `WIM_WhoInfo()` - Added debug messages
- Modified `playerCheck()` - Skip WHO for known GMs
- Modified `WIM_ChatFrame_OnEvent()`:
  - `CHAT_MSG_WHISPER` - Detect GM flag, set `isGM`, update window
  - `CHAT_MSG_WHISPER_INFORM` - Detect GM flag when whispering to GM
- Modified `WIM_PostMessage()` - Skip WHO for GMs, show GM info immediately
- Modified `WIM_SetWhoInfo()` - Show GM icon/title/label for GMs, return early
- Modified `WIM_AddToHistory()` - Save `isGM` flag in history entries
- Modified `WIM_DisplayHistory()` - Display `<GM>` tag from saved history

### WIM_Hooks.lua
- Modified `WIM_FriendsFrame_OnEvent()`:
  - Added debug messages for WHO_LIST_UPDATE
  - Added `return` statement to prevent WHO window from opening
  - Check for GM status before updating WHO info

### WIM_Options.xml
- Hidden "Block Low Level Whispers" checkbox (incompatible with TurtleWoW)

## Technical Details

### GM Detection Methods
1. **Own GM Status**: Checks spellbook for "Teleport to GM Island" spell at login
2. **Other GM Status**: Server sends `arg6 = "GM"` flag with whisper events

### WHO Queue System
- Global 30-second cooldown between WHO requests (TurtleWoW limit)
- Round-robin queue prioritizes players with fewer attempts
- Maximum 5 attempts per player before removal from queue
- GMs bypass the cooldown but still wait for WHO response

### Event Flow (Normal Player)
1. Receive whisper → Display message immediately
2. Queue WHO request → Wait for 30s cooldown
3. WHO response → Update window with class/race/level

### Event Flow (GM Whisper)
1. Receive whisper with `arg6 = "GM"`
2. Set `isGM = true` in player cache
3. Display message with `<GM>` prefix
4. Skip WHO request → Show GM icon and "Game Master" label

## Changelog

### v1.0.0-TurtleWoW
- Initial TurtleWoW fork
- Added 30-second WHO cooldown
- Added GM detection and display
- Added debug mode
- Removed Block Low Level option
- Fixed WHO window popup issue
- Added GM status to history

## Credits

- Original WIM addon authors
- TurtleWoW community
- Modified for TurtleWoW by [Your Name]

## License

See original WIM license.
