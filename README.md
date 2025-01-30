| Platform | Issue                                                       | Solution                                                             | Extra Info                                                                                                                                                                                                                       |
|----------|-------------------------------------------------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| All      | SSH: `'xterm-ghostty': unknown terminal type`               | docs (help > terminfo)                                               |                                                                                                                                                                                                                                  |
| All      | Scripting Ghostty events                                    | #2535                                                                |                                                                                                                                                                                                                                  |
| All      | Scroll Bar                                                  | #189                                                                 |                                                                                                                                                                                                                                  |
| All      | Mouse Action Mapping                                        | #3848                                                                |                                                                                                                                                                                                                                  |
| All      | `plus` mapping as `shift`+`plus` instead of `shift`+`equal` | #4007 `kitten show-key -m kitty`                                     | https://www.leonerd.org.uk/hacks/fixterms/ https://sw.kovidgoyal.net/kitty/keyboard-protocol/                                                                                                                                    |
| All      | `sudo` : `'xterm-ghostty': unknown terminal type`           | docs (option > shell-integration-features)                           | `sudo` is not part of the default Ghostty shell integration                                                                                                                                                                      |
| All      | `tmux` : `alt` keybindings no longer work                   | `ghostty +list-keybinds \| grep alt`                                 | Ghostty ships with some keybinds by default that will interfere with `tmux`.  Unbind them or change your `tmux` binds.                                                                                                           |
| All      | Various `font-feature` options                              | docs (option > font-feature) [FontDrop](https://fontdrop.info)       |                                                                                                                                                                                                                                  |
| MacOS    | Pointer shape/style for column selection (crosshair)        | #5384                                                                |                                                                                                                                                                                                                                  |
| MacOS    | Open configuration file using $EDITOR (not TextEdit)        | #2961                                                                |                                                                                                                                                                                                                                  |
| MacOS    | Aerospace issues with Ghostty (native tabs)                 | docs (help > macos-tiling-wms) Aerospace #68                         |                                                                                                                                                                                                                                  |
| MacOS    | Quit Ghostty after last surface is closed                   | docs (option > quit-after-last-window-closed)                        |                                                                                                                                                                                                                                  |
| MacOS    | `clear` also purges the scrollback buffer                   | #5269                                                                | TL;DR: Use `ctrl`+`l` OR do some aliasing.  If your `$TERM` supports E3 (Ghostty does) macOS clear/ncurses will make it clear the buffer.                                                                                        |
| MacOS    | Intel Macs - flashing/graphical bugs                        | https://discord.com/channels/1005603569187160125/1325428198078681150 | A custom no-op shader will address some of the graphical issues.  Sadly, Apple has pretty much sunset the Intel embedded graphics development and patches in favor of Apple Silicon, so there's no official fix/patch available. |
| MacOS    | Mission Control Lag                                         | #4256 #4316                                                          |                                                                                                                                                                                                                                  |
