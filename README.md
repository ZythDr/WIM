# WIM 1.4.0 - TurtleWoW

## Patch Notes

### New Features
- **New Filter Type: Exact** – Now filters only whispers matching exactly. "inv" only blocks message "inv", still allows message like "raid inv now"
- **Unfocus WIM Window** – Pressing Escape now leaving window focus but keeps insert text. Optional under general with "escape close window" dependency.
- **Alt+Arrow Key Toggle** – Added option to text cursor moving. Alt modifier now can be disabled to work like in normal inputbox.

### Bug Fixes
- **Ingame Links** – All chat links such as items, spells, quests, etc. now insert correctly without gaps.
- **Macro Whispers** – Script- and macro-based whispers now send and display correctly in WIM.
- **Filter Iteration** – Fixed Lua 5.0 table iteration to now properly use `pairs()`, preventing undefined behavior.

### UI Improvements
- Reorganized General options for improved clarity and better accessibility
- Updated code formatting across all checkboxes for consistency

Some more minor quality of life changes. 🐢

## Previous Changes
- Added 30s WHO cooldown (TurtleWoW limit)
- Messages now display immediately (WHO loads async)
- Removed "Block Low Level" option
- Added debug mode: `/wimdebug`
