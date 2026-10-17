# Troubleshooting

## Finish Setup says the game is missing

In the included Windows Steam client, sign in to the account that owns Hood Warfare 2 and finish its download. The Steam app ID is `5155360`. Finish Setup waits for both the installed-game manifest and the game executable. Keep the game in this client's default Steam library.

Run `Finish Setup.command` again when the download is complete. It closes this setup's Windows Steam client before saving the game's launch option, and backs up the configuration first.

## Switching Steam accounts

Open `Open Windows Steam.command` and sign in to the other account privately. That account must own the game. Run `Finish Setup.command` again to save the required launch option for the newly signed-in account.

## Download checksum mismatch

Installation stops when a download does not match its pinned SHA-256. Get the [latest project release](https://github.com/SPACEMATES-STUDIO/hood-warfare-2-on-mac/releases/latest), then retry. If the message identifies a corrupt cached file, remove only that named file from `~/Library/Caches/hood-warfare-2-on-mac` and retry. A persistent mismatch needs a reviewed update to the project's download pin; do not bypass the check.

## Microsoft Visual C++ prerequisite dialog

Run `Finish Setup.command`, then open `Hood Warfare 2.app`. On the tested build, the Unreal Engine bootstrap incorrectly reported a missing runtime even with Microsoft Visual C++ x64 14.51.36247 installed.

The configured Steam launch option is:

```text
C:\windows\system32\cmd.exe /d /c C:\HoodWarfare2-launch.cmd %command%
```

This starts the original game executable through Steam and skips only that faulty prerequisite bootstrap. No game files are patched. An older redistributable reporting that a newer version is installed is not a reason to downgrade.

## Steam is black or does not open

Use `Open Windows Steam.command` from this installation and allow the first Steam update to finish. This setup supplies the Wine engine's matching libraries and DXMT/D3DMetal configuration. Copying only the Wine executable or using a different Wine installation can fail before a window appears.

The tested setup uses Steam's default rendering options. Do not add old Chromium GPU-disabling flags as a first troubleshooting step.

## Steam or Wine keeps reopening

Close Hood Warfare 2, then open `Quit Windows Steam.command` in the installation folder. You can also choose **Steam → Exit inside the Windows Steam window**. Closing or quitting a Wine window can leave Steam's main process running; Steam can restart its window helper.

The Quit shortcut requests a normal Steam shutdown, waits for Steam to exit, then stops only this installation's remaining Wine helpers. It refuses to stop a running game. It does not open Steam when the session is already stopped, and it leaves macOS Steam and other Wine installations alone. If setup is still waiting for a download, cancel that Terminal window with Control-C before using Quit.

If your installation lacks the Quit shortcut, download the latest release and rerun `Install.command` with the same destination. This preserves the downloaded game and Steam account. To update without launching the game afterward, run `./Install.command --no-open` from the unzipped release folder in Terminal (add `--destination '/your/install/folder'` for a custom destination).

## Controller letters or positions seem reversed

Open `Controller Layout.command` and choose your preference:

- Standard button positions: start here for Xbox, PlayStation, and other supported gamepads; the bottom face button acts as the primary confirm button.
- Match printed button letters: follow the controller's printed A/B/X/Y labels where supported.
- Keyboard and mouse: no controller setup is needed.

Restart the game environment as the command instructs. Use `Test Controller.command` and press physical buttons to check their reported values. The Windows tester keeps an Xbox-shaped illustration regardless of your controller's shape or selected layout.

There is no controller-brand restriction in the installer. Detection depends on your controller, connection, macOS, and Wine. Connect the controller before launching Steam and check it with `Test Controller.command`; changing the layout cannot make an undetected device appear. Individual models have not all been tested.

The Switch Pro controller was detected through Wine as an XInput controller. Physical-button and in-game controller verification remain pending; detection alone does not confirm every binding. Steam Input was left at its default setting during the original setup.

## Multiplayer stops working after an update

Use Windows Steam to update the game and verify its installed files. Check the game's current server status and release notes. Public multiplayer was tested on build `25888787`; future updates can change compatibility. This project provides no anti-cheat bypass.

## Friends cannot join a party

[Patch 1.0.1.7](https://store.steampowered.com/news/app/5155360/view/672882996184876027) added party invitations and the ability to queue and join games together. Instructions written before that patch may describe missing invitation support.

1. Close the game and open this installation's `Open Windows Steam.command` to check for updates. Have the other players update too; updating macOS Steam alone does not update this Windows installation.
2. Use the game's party invitations and confirm that everyone has joined the party before starting matchmaking. Entering matchmaking separately is not a substitute for joining a party.
3. If it still fails, note which step fails: sending the invitation, receiving or accepting it, or joining a match after queuing. Include that detail and each player's game build when reporting the problem.

The patch announcement confirms joining games together, but does not promise assignment to the same team. It also does not establish that party invitations work through this Mac/Wine setup; the project's earlier public-multiplayer test is a separate result.

For a longer game-level checklist, including the difference between party matchmaking and password-protected private matches, see the [unofficial Hood Warfare 2 friends guide](https://hoodwarfare2.run/hood-warfare-2-friends/). It is a community-maintained resource, not evidence of Mac compatibility.

## Uninstalling

Quit the game and its Windows Steam client, then remove `~/Applications/Hood Warfare 2 on Mac` (or the custom destination you selected). This also removes the downloaded game, this installation's Wine prefix, and its local saves; copy any saves you want to keep first.

You can also remove this installer's download cache at `~/Library/Caches/hood-warfare-2-on-mac`, or the custom cache selected at installation, to reclaim that space.

## Reporting a problem

Include your Mac chip, macOS version, game build, the command you opened, and the exact error. Review any log excerpt before posting it publicly. Do not upload the Wine prefix, Steam account configuration, or sign-in data.
