# PopOut!

PopOut! adds a button to most Foundry VTT actor sheets, item sheets, journal entries, and application windows so they can be opened in a separate browser window. It is useful for multi-monitor setups or for keeping frequently referenced sheets visible while working elsewhere in Foundry.

This fork is a Foundry V14 compatibility bridge for users whose game systems still use legacy Application V1 sheets. Foundry V14 has native pop-out support for ApplicationV2 apps, but legacy V1 actor and item sheets do not automatically receive that native button.

**Support:** If this compatibility fork helps your Foundry V14 workflow, donations are optional and support Spencer's compatibility testing, release packaging, and documentation. Upstream author and maintainer credit remains below.

[![Sponsor on GitHub](https://img.shields.io/badge/GitHub%20Sponsors-Donate-ea4aaa?style=flat&logo=githubsponsors&logoColor=white)](https://github.com/sponsors/SpencerZPoole) [![Donate with PayPal](https://img.shields.io/badge/PayPal-One--time%20donation-00457C?style=flat&logo=paypal&logoColor=white)](https://paypal.me/mrpooley92)

## Who Should Use This Fork?

Use this fork if all of the following are true:

- You are running Foundry V14 in a regular browser.
- Your game system still uses legacy Application V1 actor, item, or document sheets.
- Foundry's native ApplicationV2 pop-out button does not appear on the sheets you actually use at the table.

This is not a replacement for Foundry's native V14 pop-out feature. It is a transition bridge for systems such as D35E, PF2e during migration, or other systems/modules whose sheets have not fully moved to ApplicationV2 yet.

This fork keeps the original module id, `popout`, so it behaves as a drop-in direct-manifest install. It is not submitted as a separate Foundry package listing.

## Install

Install this fork from Foundry's **Add-on Modules** screen with this manifest URL:

```text
https://github.com/SpencerZPoole/fvtt-module-popout/releases/latest/download/module.json
```

The release zip for this build is:

```text
https://github.com/SpencerZPoole/fvtt-module-popout/releases/download/v2.24.1/module.zip
```

After installation, enable **PopOut!** in your world's **Manage Modules** menu.

## Compatibility

- Module version: `2.24.1`
- Foundry minimum: `12`
- Verified with Foundry: `14.362`
- Tested environment: Foundry `14.362` with the D35E system `3.0.2`
- Browser support: regular web browsers only

Foundry V14's native pop-out support is ApplicationV2-based. This fork remains useful where your system's live sheets are still legacy V1 applications and therefore do not expose the native pop-out control.

PopOut! does not work in Foundry's Electron desktop application window. If you host Foundry locally, use a browser such as Chrome pointed at your Foundry server instead.

PopOut! works by moving Foundry application DOM nodes into another browser window. That makes broad compatibility possible, but some sheets or modules that rely heavily on global `document` lookups, jQuery plugins, React, Svelte, Vue, or other framework-specific assumptions may still have limitations when popped out.

## Changes In This Fork

### `2.24.1`

- Clarified this fork's public purpose: a Foundry V14 bridge for systems still using legacy Application V1 sheets.
- Documented that Foundry V14 native pop-outs exist for ApplicationV2 apps and this fork only fills the remaining V1-sheet gap.
- Confirmed the fork is distributed through GitHub releases and direct manifest install, not as a separate Foundry package listing.
- Updated the upstream status: compatibility pull request [#164](https://github.com/League-of-Foundry-Developers/fvtt-module-popout/pull/164) was closed unmerged, and upstream issue [#165](https://github.com/League-of-Foundry-Developers/fvtt-module-popout/issues/165) tracks the legacy V1-sheet use case.

### `2.24.0`

- Verified PopOut! against Foundry `14.362`.
- Updated module compatibility metadata for Foundry V14 and removed the stale maximum-version cap.
- Published release assets for direct installation from this public fork.
- Incorporated the keyboard focus fix from upstream PR [#163](https://github.com/League-of-Foundry-Developers/fvtt-module-popout/pull/163), credited to Sigiller, so typing in popped-out input fields is less likely to trigger Foundry hotbar digit shortcuts.
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

PopOut! was written by KaKaRoTo and maintained by Posnet and the League of Foundry Developers. This compatibility fork preserves the original module id, history, and attribution.

This module is licensed under the Foundry Virtual Tabletop module development license terms and the Creative Commons Attribution 4.0 International License where applicable. See [LICENSE.txt](./LICENSE.txt).
