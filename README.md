# studio-linux-themes

Theme packs for [studio-linux](https://github.com/Codys-Wright/studio-linux). Nothing here is needed to
build a machine: themes are installed at runtime with the `studio` CLI.

```sh
studio theme install github:Codys-Wright/studio-linux-themes#<name>
studio theme install qylock:<theme>      # importer — fetched from upstream at install time
studio theme install cozytile:<theme>    # importer — Cozy, Sakura, Natura, Everforest, Carbon
```

A pack is a directory under `packs/<name>/`:

| File | Required | Contents |
|---|---|---|
| `manifest.json` | yes | name, author, version, license, source |
| `theme.json` | yes | `palette` (base colors + semantic roles, polarity) and `glass` (blur, xray, tint, opacity) |
| `wallpaper.*`, `fonts/`, `lock/`, `greeter/`, `apps/` | no | fall back to the default theme's |

The format is specified in the studio-linux [plan](https://github.com/Codys-Wright/studio-linux/blob/main/docs/PLAN.md#42-theme-system-engine-packs-manager-studio-linux-theme-engine) (§4.2) and will move here once it stabilises.

## Vibes

`index.json` `"vibes"` groups packs that share a look. Every pack of a group gets the other members'
wallpapers and lock designs as curated suggestions (`studio theme vibes <pack>`, the shell's wallpaper
and lock pickers), shown before the palette-ranked matches. Only installed packs are used; a group may
name packs that aren't installed (yet).

```json
{ "name": "sakura", "packs": ["cozytile-sakura", "qylock-pixel-sakura"],
  "wallpapers": ["<pack>:<file>"], "locks": ["<pack>:<lock name>"] }
```

`wallpapers` / `locks` (optional) add specific assets to every member. The importers copy a pack's
links into its `manifest.json` (`vibes`) so they also hold offline; `studio` reads this index from
`$STUDIO_THEME_INDEX` (a path or URL, `none` to disable), by default this file on GitHub (cached a day).
