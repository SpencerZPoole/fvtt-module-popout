# PopOut!

PopOut! adds a button to most Foundry VTT actor sheets, item sheets, journal entries, and application windows so they can be opened in a separate browser window. It is useful for multi-monitor setups or for keeping frequently referenced sheets visible while working elsewhere in Foundry.

## Install

In Foundry, open **Add-on Modules > Install Module**, paste a manifest URL into **Manifest URL**, and install.

Official upstream channel:

```text
https://raw.githubusercontent.com/League-of-Foundry-Developers/fvtt-module-popout/master/module.json
```

Spencer's Foundry V14 compatibility build:

```text
https://github.com/SpencerZPoole/fvtt-module-popout/releases/latest/download/module.json
```

After installation, enable **PopOut!** in your world's **Manage Modules** menu.

## Compatibility

- Module version: `2.24.0`
- Foundry minimum: `12`
- Verified with Foundry: `14.362`
- Browser support: regular web browsers only

PopOut! does not work in Foundry's Electron desktop application window. If you host Foundry locally, use a browser such as Chrome pointed at your Foundry server instead.

PopOut! works by moving Foundry application DOM nodes into another browser window. That makes broad compatibility possible, but some sheets or modules that rely heavily on global `document` lookups, jQuery plugins, React, Svelte, Vue, or other framework-specific assumptions may still have limitations when popped out.

## Changes

### `2.24.0`

- Verified PopOut! against Foundry `14.362`.
- Updated module compatibility metadata for Foundry V14 and removed the stale maximum-version cap.
- Incorporated the keyboard focus fix from PR [#163](https://github.com/League-of-Foundry-Developers/fvtt-module-popout/pull/163), credited to Sigiller, so typing in popped-out input fields is less likely to trigger Foundry hotbar digit shortcuts.
- Preserved the existing PopOut! module id, behavior, hooks, and browser-only warning.

## Module Developer Notes

If your module accesses HTML through global document lookups such as `document.getElementById(...)`, `document.querySelector(...)`, or `$(...)`, it may not find elements after an application is popped out. Prefer searching from the application element itself, for example:

```js
sheet.element.find(".my-control");
```

To prevent PopOut! from handling an application, set `_disable_popout_module` on the application or pass `popOutModuleDisable` in the application options.

```js
Dialog.prompt({ title: "", options: { popOutModuleDisable: true } });
```

PopOut! also exposes `PopoutModule.popoutApp(app)` and the existing PopOut hooks:

- `PopOut:popout`
- `Popout:loading`
- `Popout:loaded`
- `PopOut:popin`
- `PopOut:dialog`
- `PopOut:close`

## Credits

PopOut! was written by KaKaRoTo and maintained by Posnet and the League of Foundry Developers.

This module is licensed under the Foundry Virtual Tabletop module development license terms and the Creative Commons Attribution 4.0 International License where applicable. See [LICENSE.txt](./LICENSE.txt).
