# Minecraft Item Editor

A standalone, browser-based editor for building Minecraft item component NBT strings — the kind used in `/give` commands, crate configs, and plugin YAML files. No install, no server, no dependencies. Just open the HTML file.

---

## Usage

Download `minecraft-item-editor.html` and open it in any modern browser. Everything runs locally.

---

## Features

### Item Settings
- **Item ID** — set the item type (e.g. `iron_block`, `diamond_sword`). The `minecraft:` prefix is added automatically if omitted.
- **Count** — stack size from 1 to 64.
- **Enchant Glint** — forces the enchantment shimmer effect without needing an actual enchantment (`minecraft:enchantment_glint_override`).
- **Hide Attributes** — suppresses the default attribute tooltip lines (`minecraft:attribute_modifiers` with `show_in_tooltip: false`).
- **Hide Tooltip** — hides the entire tooltip (`minecraft:hide_additional_tooltip`).

### Display Name
Edit the item's custom name as one or more **segments**. Each segment is an independent piece of text with its own formatting, allowing multi-colored names on a single line.

### Lore
Add as many lore lines as needed. Each line supports multiple segments, same as the display name. Empty lines act as spacers in the tooltip.

### Per-Segment Formatting
Every segment (in both name and lore) has:

| Control | Description |
|---|---|
| Color swatch | Click to open the browser's native color picker |
| Color dropdown | Choose from all 16 named Minecraft colors |
| ⬡ Hex | Switch to custom hex mode, type any `#RRGGBB` value |
| **B** | Bold |
| *I* | Italic |
| ~~S~~ | Strikethrough |
| U | Underlined |
| O | Obfuscated (scrambled) |

Named colors and hex colors (`#RRGGBB`) both output correctly. Hex requires Minecraft 1.16+.

### Live Preview
The right panel renders a Minecraft-style tooltip in real time as you edit, including the purple border, dark background, and pixel font.

### Paste Existing Value
Click **paste existing value** at the top to load an item you already have. Paste in either format:

```
Value: '{components:{...},count:1,id:"minecraft:stone"}'
```
```
{components:{...},count:1,id:"minecraft:stone"}
```

The parser handles `1b`/`0b` booleans, unquoted NBT keys, and literal newlines in text values.

### Output
The generated NBT updates live as you edit. Two copy buttons are available:

- **copy nbt** — raw NBT string, ready to use in `/give` or code
- **copy as Value: '...'** — wrapped format for direct paste into YAML plugin configs (CrateReloaded, etc.)

---

## Output Format

The editor generates the Minecraft 1.20.5+ components format:

```
{components:{"minecraft:custom_name":{extra:[{bold:1b,color:"green",...,text:"My Item",...}],text:""},"minecraft:lore":[...]},count:1,id:"minecraft:stone"}
```

---

## Compatibility

- Minecraft **1.20.5+** (components format)
- Hex colors require **1.16+**
- Works in any modern browser (Chrome, Firefox, Edge, Safari)
- No internet connection required after the font loads on first open

---

## Notes

- The `minecraft:` prefix on item IDs is optional — the editor adds it automatically.
- Segment order matters: segments render left to right on the same line.
- Empty lore lines (all segments with blank text) render as vertical spacing in the tooltip.
- Obfuscated text shows as `▒` blocks in the preview — in-game it animates.
