# 🎨 Local Account Skin Apply

Client-side **skin & cape manager** for **offline** Minecraft Java 1.8.9 accounts 🧱
Built for **Forge 11.15.1.2318** on **Java 8** ☕

📱 Works with **PojavLauncher**, **MJ Launcher** and standard Forge 1.8.9 installs.
🌐 No internet, no Mojang/Microsoft API, no backend.

---

## ✨ Features

- 🖥️ Compact, native Minecraft-style GUI (`/skin`)
- 🧍 Separate **Skin Manager** and 🧣 **Cape Manager**
- 🔄 Real **3D player preview**: drag to rotate, plus Front / Side / Back buttons
- 🏷️ Assign a skin or cape to any offline username, in game or by naming the PNG
- 🖼️ Supports 64x64, legacy 64x32 and HD skins (128x128, ...)
- 💪 Slim (Alex) arms detected automatically
- 🧣 Supports 64x32, 22x17 and 46x22 capes (and multiples)
- 💾 Assignments saved in `config.json`, kept after restart
- ⚠️ Apply popup with exactly two buttons: **EXIT** and **CANCEL**
- 🚫 No automatic restart, ever
- 🪶 Lightweight: no extra libraries, no background threads, no polling

---

## 📦 Install

1. ✅ Install Minecraft 1.8.9 with Forge 11.15.1.2318
2. 📥 Install [LocalAccountSkinApply-1.0.0.jar](              into `.minecraft/mods`
3👍 [LocalAccountSkinApply-Source.zip](
4. ▶️ Start the game

---

## 📁 Folders

Created automatically on first launch in the real game directory:

```
.minecraft/LocalAccountSkinApply/
├── Skins/         🧍 PNG skins
├── Capes/         🧣 PNG capes
└── config.json    📝 username -> file assignments
```

🔁 Deleted folders are recreated on the next launch.

---

## 🛠️ Two ways to assign

Both use the same assignment table.

### 🎮 Method A: in game

1. ⌨️ Type `/skin`
2. 👆 Open **SKINS** or **CAPES**
3. 📄 Select a PNG
4. ✏️ Click **Rename** and enter the offline username (e.g. `Steve123`)
5. ✅ Click **Apply**

### 📂 Method B: file manager

Name the PNG after the username:

```
Skins/
├── Steve123.png
├── Alex.png
└── Player01.png
```

🔄 Press **Refresh** in the GUI, or rejoin the world.

⚠️ If the username is already used by a different PNG, the first **Apply** warns you and a second **Apply** replaces it.

---

## 💬 Commands

All commands are client side and send no chat messages.

| Command | What it does |
|---|---|
| `/skin` 🎛️ | Opens the main menu (LOCAL ACCOUNT SKIN APPLY: SKINS / CAPES) |
| `/default` 🧍 | Restores the default skin for the current player (skin only) |
| `/reset` ♻️ | Clears the current player's skin **and** cape assignments |

🛡️ None of these delete PNG files. **Remove** in the manager only removes the assignment.

ℹ️ A PNG named after your username stays unassigned after `/default`, `/reset` or Remove until you replace/rename the file or assign it again.

---

## 🪟 Apply popup

After **Apply**, a centered in-game popup appears:

> ❓ Are you sure you want to exit and rejoin?

| Button | Behavior |
|---|---|
| 🚪 **EXIT** | Saves, then closes Minecraft normally. You start the game again yourself. |
| ❌ **CANCEL** | Closes the popup. The game keeps running and the assignment stays saved. |

---

## ⚙️ How it works

Minecraft 1.8.9 reads each player's skin, cape and model type from `NetworkPlayerInfo`. The mod registers your PNGs as `DynamicTexture`s and writes them into that object right before a player is rendered (`RenderPlayerEvent.Pre` and `RenderHandEvent`). 🧩 No coremod or ASM needed.

- 🔧 Legacy 64x32 skins are converted like vanilla
- 🧣 22x17 and 46x22 capes are converted to the 64x32 layout
- 🧍 The 3D preview renders a temporary `EntityOtherPlayerMP` through `RenderManager` (same idea as `GuiInventory`)
- 🧹 Textures are cached, freed when files change or disappear, and capped at 24

---

## ⚠️ Limitations

- 👥 Other players only see your skin/cape if their clients also run this mod with the same files
- 🖥️ Assignments apply on your client only, to any player whose name matches
- 🎯 Minecraft 1.8.9 with Forge 11.15.1.2318 only

---

```

## 📋 Project info

| Item | Value |
|---|---|
| 🏷️ Mod name | Local Account Skin Apply |
| 🆔 Mod ID | `localaccountskinapply` |
| 🔢 Version | 1.0.0 |
| 🎮 Minecraft | 1.8.9 |
| 🔨 Forge | 11.15.1.2318 |
| ☕ Java | 8 |
| 🧰 ForgeGradle | 2.1 |
| 🐘 Gradle | 2.14.1 |
| 🖥️ Side | Client only |
