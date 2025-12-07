# ZombieKiller Mod for PEAK by Uni

A BepInEx mod that allows you to kill zombies in PEAK with a configurable hotkey.

## Features

- **Kill zombies instantly** with a single keypress
- **Two modes:**
  - **Radius Mode**: Kill zombies within a specific radius around you
  - **Kill All Mode**: Kill ALL zombies on the map regardless of distance
- **Configurable hotkey, radius, and cooldown**
- **Uses horizontal distance** (ignores height differences) - perfect for mountain climbing!
- **Debug logging** to help you see what's happening

## Installation

1. **Install BepInEx** (if you haven't already)
   - Download BepInEx 5.x from [GitHub](https://github.com/BepInEx/BepInEx/releases)
   - Extract to your PEAK game folder
   - Run the game once to generate BepInEx folders

2. **Install the mod**
   - Download `ZombieKiller.dll`
   - Place it in: `PEAK/BepInEx/plugins/`

3. **Launch the game**
   - The mod will create a config file on first launch
   - Config location: `PEAK/BepInEx/config/com.zombiekiller.cfg`

## Usage

**Default Controls:**
- Press **K** to kill nearby zombies

**In-Game:**
1. Spawn zombies using the zombie spawner mod (J key)
2. Press **K** to kill zombies within range
3. Check the BepInEx console for feedback

## Configuration

Edit `BepInEx/config/com.zombiekiller.cfg`:

```ini
[General]

## Key to kill zombies
# Default: K
KillKey = K

## Radius to kill zombies (in meters). Only used if KillAll is false.
# Default: 50.0
KillRadius = 50.0

## If true, kills ALL zombies on the map. If false, only kills zombies within KillRadius.
# Default: false
KillAll = false

## Cooldown between uses (in seconds)
# Default: 1.0
CooldownSeconds = 1.0

## Enable detailed debug logging
# Default: true
DebugMode = true
```

### Configuration Examples

**Kill all zombies instantly:**
```ini
KillAll = true
```

**Increase kill range:**
```ini
KillRadius = 100.0
```

**Change hotkey to L:**
```ini
KillKey = L
```

**Remove cooldown:**
```ini
CooldownSeconds = 0.0
```

## How It Works

The mod:
1. Finds all `Character` objects in the scene
2. Checks if each character is a zombie (`character.isZombie`)
3. Calculates **flat/horizontal distance** (ignoring height) from your position
4. Kills zombies within range by setting their `_dead` field to `true`

**Distance Calculation:**
- Uses 2D flat distance (X and Z axes only)
- Ignores Y-axis (height) to work properly while climbing
- Perfect for PEAK's mountainous terrain!

## Troubleshooting

### Zombies aren't being killed
- **Check the console/log** for debug messages
- Make sure you're within `KillRadius` of the zombie
- Try increasing `KillRadius` in the config
- Or set `KillAll = true` to kill all zombies regardless of distance

### "No zombies found to kill"
- Spawn a zombie first using the zombie spawner mod (J key)
- Make sure the zombie is within your kill radius
- Check that the zombie spawned near you, not far away

### Position issues
- If the mod thinks you're far away when you're not, check the debug log
- The mod should show "Using Head position" in debug mode
- If issues persist, try `KillAll = true` as a workaround

### Cooldown active
- Wait for the cooldown to finish (shown in console)
- Or reduce `CooldownSeconds` in the config

## Debug Information

With `DebugMode = true`, the console will show:
- Your current position when pressing K
- Distance to each zombie (flat distance)
- Which zombies are within range
- Which kill method was used (Die method, _dead field, or GameObject destroy)

## Compatibility

- **Requires:** BepInEx 5.x
- **Game Version:** Built for PEAK (Unity 6000.0.36)
- **Works with:**
  - Zombie Spawner mod (recommended)
  - Other PEAK mods

## Version History

### v1.0.0 (Initial Release)
- Kill zombies with hotkey
- Configurable radius and kill-all modes
- Flat distance calculation for mountain climbing
- Debug logging

## Credits

- **Author:** Uni
- **Based on:** Zombie Spawner mod structure
- **Framework:** BepInEx

## Support

If you encounter issues:
1. Enable `DebugMode = true` in the config
2. Check the BepInEx console or log file: `BepInEx/LogOutput.log`
3. Share the relevant log sections for help

## License

Free to use and modify for personal use.

---

**Have fun eliminating zombies on PEAK! 🧟‍♂️⛰️**
