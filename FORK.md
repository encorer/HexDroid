# Changes in this fork

This is a personal fork of [boxlabss/HexDroid](https://github.com/boxlabss/HexDroid), based on upstream **v1.7.8** (commit `08de699`). It adds a few small quality-of-life changes for a quieter chat. Everything else is unchanged from upstream.

## 1. Hide account login lines

New **Account logins** chip in **Settings → Chat → Channel events** (and in each channel's own settings).

When turned off, lines from IRCv3 `account-notify` are no longer shown in channels:

```
* aduskett is now logged in as aduskett
* aduskett logged out
```

Your own login and logout lines are always shown.

## 2. Hide your own "Now talking on" line

New **Your joins** chip in the same place.

When turned off, the line printed when you join a channel is hidden:

```
* Now talking on #news
```

Other people's joins are still controlled by the existing **Joins** chip. Turning **Joins** off hides your own join line too, as before.

## 3. Keyboard no longer reopens after switching apps

Before: tap the message field, close the keyboard with Back or a swipe, switch to another app and back, and the keyboard pops up again by itself.

Now: closing the keyboard also removes focus from the message field, so it stays closed until you tap the field again. If you leave the app with the keyboard open, it is restored as before. Nothing changes with a hardware keyboard.

## Already in upstream

Mode changes (`*** nick sets mode -b ...`) and nick changes (`* old is now known as new`) can be hidden with the **Mode changes** and **Nick changes** chips. Those were added upstream in v1.7.8.

## Building

```bash
./gradlew assembleDebug
```

The APK is written to `app/build/outputs/apk/debug/app-debug.apk`. Its package name is `com.boxlabs.hexdroid.debug`, so it installs alongside the official app instead of replacing it.

## Files touched

- `IrcViewModel.kt`, `IrcViewModelFilters.kt`: new `ACCOUNT` and `OWN_JOIN` event kinds
- `IrcViewModelStateEvents.kt`: account-notify lines respect the filter
- `IrcViewModelChannelEvents.kt`: own join line respects the filter
- `UiState.kt`, `data/ChannelPrefs.kt`, `data/SettingsRepository.kt`: new `hideAccountChanges` and `hideOwnJoins` settings (default off, so existing settings are unaffected)
- `ui/ChannelEventChips.kt`: the two new chips
- `ui/ChatScreen.kt`: keyboard focus fix
- `res/values*/strings.xml`: chip labels in all 16 languages

## License

GPL-3.0, same as upstream. See [LICENSE](LICENSE).
