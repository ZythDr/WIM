# WIM - TurtleWoW Fork

Modified WIM for TurtleWoW with cross-faction whisper support and GM detection.

## Changes

- **30s WHO cooldown** (TurtleWoW limit)
- **GM detection** - Shows Blizzard icon, `<GM>` tag, "Game Master" label
- **GMs skip WHO cooldown**
- **Messages display immediately** - WHO info loads async
- **Removed "Block Low Level"** option (cross-faction incompatible)
- **Debug mode** - `/wimdebug`

## Files Modified

- `WIM.lua` - WHO queue, GM detection, debug system
- `WIM_Hooks.lua` - WHO_LIST_UPDATE handling
- `WIM_Options.xml` - Hidden Block Low Level checkbox
