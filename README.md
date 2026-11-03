<h1 align="center">Persona Quickshell</h1>

<div align="center">

[![QML](https://img.shields.io/badge/QML-Quickshell-7aa2f7?style=for-the-badge&logo=qt&logoColor=white)](https://quickshell.outfoxxed.me)
[![Stars](https://img.shields.io/github/stars/Yujonpradhananga/Persona-Quickshell-?style=for-the-badge&color=e0af68&logoColor=white)](https://github.com/Yujonpradhananga/Persona-Quickshell-/stargazers)
[![Hyprland](https://img.shields.io/badge/Hyprland-supported-2ac3de?style=for-the-badge&logoColor=white)](https://hyprland.org)
[![Last Commit](https://img.shields.io/github/last-commit/Yujonpradhananga/Persona-Quickshell-?style=for-the-badge&color=9ece6a&logoColor=white)](https://github.com/Yujonpradhananga/Persona-Quickshell-/commits/main)

</div>



<https://github.com/user-attachments/assets/7e6fd291-dd28-48fa-83aa-81556558b132>







---

## Dependencies

### Plugins

A custom cava plugin is used here:
**Link:** <https://github.com/Yujonpradhananga/Qt6-Cava-plugin>

You can build the plugin mannually or if you dont want to mannually build it and go through the installation process you can delete the `CavaVisualizer.qml` file and delete these lines 171-180 from the `WallpaperEngine.qml` file:

```qml
//delete these
CavaVisualizer {
  id: s1_cava
  anchors {
    left: parent.left
    right: parent.right
    top: parent.top
    topMargin: 0
  }
  height: 555
}
```
---

## AppLauncher

The AppLauncher requires a hyprland keybind for it to work.
Mine is set like this:

```lua
hl.bind(
    mainMod .. " + R",
    hl.dsp.exec_cmd("qs -c /path to where you have installed the repo/Persona-Quickshell/ ipc call searchapp toggle")
)
```

---

## Credits
The wallpaper is from : https://steamcommunity.com/sharedfiles/filedetails/?id=3151551777

The greyscale shader is from [@snes19xx](https://github.com/snes19xx)'s [surface-dots](https://github.com/snes19xx/surface-dots/blob/main/.config/hypr/shaders/reading_mode.glsl).

The media player's album art implementation is taken from [Rexcrazy804](https://github.com/Rexcrazy804)'s [Zaphkiel](https://github.com/Rexcrazy804/Zaphkiel).

Shoutout to [blairxu13](https://github.com/blairxu13)'s [persona3-website](https://github.com/blairxu13/persona3-website).
## Power Menu

Shutdown and restart use `systemctl poweroff` and `systemctl reboot`. Logout uses `loginctl terminate-session self`.

---

## License

MIT License - feel free to use and modify as needed.

Created by Yujon Pradhananga

## Dependencies and repair notes

Options uses installed **Bebas Neue** and **Montserrat** font families rather than
loading absent font files from Assets/fonts. The volume and brightness icons use
**Symbols Nerd Font**. Media controls also need **Material Symbols Rounded**;
a Nerd Font does not replace that font.

On Arch, Montserrat and the OSD symbol font are available with:

```bash
sudo pacman -S --needed ttf-nerd-fonts-symbols ttf-montserrat
fc-cache -f
```

Use `fc-match -f '%{family}\\n' 'Bebas Neue'` (or another requested family) to
check font resolution. If a different family is returned, install the requested
font separately. Other theme components request Linux Biolinum, Microsoft Yahei,
Bahnschrift Condensed and proggyfonts; these are not bundled and may be substituted.

| Feature | Dependency |
| --- | --- |
| Wi-Fi status and scanning | NetworkManager and nmcli |
| Bluetooth status | BlueZ and Quickshell Bluetooth support |
| Battery status | UPower and Quickshell UPower support |
| Volume | PipeWire, a session manager such as WirePlumber, and Quickshell PipeWire support |
| Media controls | An active MPRIS player |
| Menu videos | Qt Multimedia and a backend/codecs supporting the bundled MP4s |
| Screen shaders | hyprctl in the active Hyprland session |
| Visualizer | Custom Cava plugin, unless CavaVisualizer has been replaced with an empty Item |

The Wi-Fi and Bluetooth lists in Stats display information; they do not currently
implement connection management.

### Repair behavior and verification

- Menu entries support clicks/taps as well as rightward drags. Canceled drags reset.
- Escape closes Options.
- Shader buttons use `hyprctl keyword decoration:screen_shader` for Hyprlang
  configurations. Lua-mode compatibility is not claimed.
- Shader command failures are logged and indicated by ERROR. ON means hyprctl
  acknowledged the request; check the display and compositor errors to verify
  shader compilation.
- Shader state tracks menu actions during the current shell instance. Changes
  made elsewhere and shell reloads may desynchronize the indicator.
- Brightness polls every 500 ms and reads the maximum when the device path loads.
  This reduces background reads, with up to half a second of OSD latency.
- Power controls execute real shutdown, reboot and logout commands. Review their
  wiring without activating them when testing other menu functions.
- Calendar placement and the wallpaper animation pipeline are retained.

Verify menu interaction, Options dismissal, shader toggles and OSD icons in a live
Quickshell/Hyprland session. Static review alone does not establish runtime behavior.
