# WebBreak

**SBPE plugins for the StarBreak web client.** By Dr. Jekyll. Current version: **beta**.

[SBPE](https://github.com/atomizer/sbpe) (StarBreak Plugin Engine) adds
zoom, a map, a custom HUD, an fps counter and more to the desktop StarBreak
client. WebBreak brings those plugins to the browser version of the game. It
uses the same `config.ini` format, the same options and the same keybinds.

You don't need to install anything. Download one patched JS file and load it
through your browser's DevTools.

## Plugins

| Plugin | What it does |
| --- | --- |
| **zoom** | Renders the game at a different internal width so you see more or less of the world |
| **map** | Minimap of the room's terrain, enemies, players, interactables and triggers |
| **extra_info** | Arrows to doors, shops, secrets, arcades, HP and boosts; trigger zone frames; object HP/armor; portal and key counts; zone name and floor |
| **hud** | Large, configurable HP/ammo/currency numbers and a health bar over your character |
| **noise** | Hides other players' shells, names, factions, health bars, objects and effects, or chat; tones down the damage flash; replaces screen shake with an indicator |
| **playerlist** | List of players in the zone: shell, mk level, name, faction |
| **fps** | FPS counter and a time reserve (network lag) indicator |
| **misc** | Centered camera (2 modes), auto-hiding cursor, background brightness cap, the game's built-in debug draw modes |
| **keybinds** | Bind any plugin option to a key |
| **version** | Shows the client and WebBreak version on the main menu |
| **ally_opacity** | Makes other players semi-transparent so you can see what's behind them. Optionally also fades their bullets, drones, damage numbers, names, emotes and effects. Ironclads stay solid while their shield is up or they're dashing |

All ten vanilla SBPE plugins are ported, plus `ally_opacity` for hiding other users.

## Install

Works in Chrome and Edge (any Chromium browser with DevTools Local Overrides).

1. Download `VR1574197275.mvmmoclient.js` from this folder or the releases section on the right side of this page. Its build number
   must match the game's current client.
2. Open the StarBreak web version and press **F12** to open DevTools.
3. Go to the **Network** tab and reload the page.
4. Right-click the `VR1574197275.mvmmoclient.js` request and choose **Override content**.
   <img width="441" height="423" alt="image" src="https://github.com/user-attachments/assets/2402f818-71f1-4af2-a7c2-76230be2fd12" />
   
6. The first time, Chrome asks for a folder to keep overrides in. Pick any
   empty folder and click **Allow**.
   <img width="940" height="519" alt="image" src="https://github.com/user-attachments/assets/c14b6a45-cbee-4301-ba97-e863e6fc6232" />
   
7. Inside the folder you chose, open the starbreak.com folder.  Then delete the `VR1574197275.mvmmoclient.js` file that is in there, and
   replace it with the file you downloaded in Step 1.
<img width="529" height="236" alt="image" src="https://github.com/user-attachments/assets/1aec1047-c3a0-428c-ac3e-9c4da1090520" />

8. Reload the game **with DevTools open.  Overrides only apply while DevTools is open.** Close DevTools and the game will load
   normally, without WebBreak

If it worked, the console shows `[WebBreak] beta by Dr. Jekyll loaded`, and
the bottom left of the main menu reads `… + SBPE WebBreak beta by Dr. Jekyll`.

### When StarBreak updates

Each game update ships a new client with a new build number in its file
name. The old WebBreak file then stops applying. You'll need the WebBreak
release for the new build.

## Default keybinds

| Key | Action |
| --- | --- |
| Right Ctrl | Show map (hold) |
| Z | Toggle zoom |
| B | Switch centered camera mode |
| V | Show player list (hold) |
| X | Toggle ally opacity |

Keybinds are ignored while you're typing in chat.

## Configure

`I have not done much testing modifying the config values.  Proceed with caution.`

The config sits at the very top of the WebBreak file, in SBPE's
`config.ini` format. To change it:

1.  Open `VR1574197275.mvmmoclient.js` in your favorite text editor.
2.  Edit the values at the top of the file then save the file.
3.  Reload the StarBreak page.

The plugins come right after the config, one block each, if you want to
tweak them.

You can turn off any plugin with `enabled = no` in its section. To add a
keybind, add a line to `[plugin_keybinds]`:

```ini
# PLUGIN OPTION TYPE VALUE [VALUE ...] = KEY
#   set    = set to value when pressed
#   hold   = first value while held, second when released
#   toggle = cycle through the values on each press
zoom level toggle -1 3000 = Z
```

To try settings without editing the file, use the DevTools console. These
changes last until you reload:

```js
WebBreak.config.set('plugin_fps', 'size', 20)
WebBreak.config.set('plugin_ally_opacity', 'opacity', 0.5)
WebBreak.config.text     // the whole config, ready to paste into the file
WebBreak.config.reset()  // back to the file's config
```

For what each option does, see the comments in the config and
[SBPE's README](https://github.com/atomizer/sbpe#configure).

### Differences from desktop SBPE

- `misc` `fixed_window` (borderless window placement) does nothing in a browser.
- `zoom` `fast` does nothing. The game always does its normal relayout when zooming.
- `[general]` (game path, mipmaps, keep_open) is not used.

## Credits

- **WebBreak** and **ally_opacity** by Dr. Jekyll.
- **SBPE** and the original plugins by [atomizer](https://github.com/atomizer/sbpe).
  WebBreak's plugins are JavaScript ports of them.
- StarBreak is made by Crunchy Games. This is an unofficial fan project.
