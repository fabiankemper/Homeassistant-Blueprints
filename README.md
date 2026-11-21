# Home Assistant Blueprints

A collection of Home Assistant automation blueprints by Fabian Kemper.


## Themes

`themes/lieblingsmubs.yaml` recolours the energy dashboard
(`/energy/electricity`, gas, water) and the general chart palette
(`graph-color-1` … `graph-color-36`), based on the
[lieblingsmubs](https://colors.fabiankemper.de/) colour scheme. Everything
else keeps the default Home Assistant look.

### Install

1. Copy `themes/lieblingsmubs.yaml` to `<config>/themes/`.
2. Enable themes in `configuration.yaml`, if not done already:

   ```yaml
   frontend:
     themes: !include_dir_merge_named themes
   ```

3. Restart Home Assistant (first time only). After that, editing the theme
   only needs **Developer Tools → YAML → Themes** (`frontend.reload_themes`).
4. Select it under **Profile → Theme** (per user and per browser), or make it
   the default for everyone:

   ```yaml
   action: frontend.set_theme
   data:
     name: lieblingsmubs
   ```

### Notes

- The `graph-color-*` palette is shared by every chart in Home Assistant,
  not only the energy panel.
- Variable names can change between frontend releases. If a colour doesn't
  apply, inspect the chart in your browser's DevTools and search the computed
  styles for `--energy-` / `--graph-color-` to get the current names.
- With several sources of one type (e.g. many grid meters), HA colours them
  from `energy-<type>-color-<index>`. If that isn't set, it darkens the base
  colour per row, which fades to grey. The theme defines
  `energy-grid-consumption-color-0` … `-35`. Other types (`solar`,
  `battery-out`, …) take the same suffix if you need them.
- Series beyond 36 use Home Assistant's built-in colours for those slots.
  To keep them on-palette, add more `graph-color-N` entries.
