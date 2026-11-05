# Nordic Nightfall appearance hook

An optional Omarchy theme hook that applies Nordic Nightfall's Files colors and
darker blue Yaru folder icons when the theme is selected. The theme's wallpapers,
palette, GTK styles, and icon assets live in the
[Nordic Nightfall theme repository](https://github.com/Z1Z0R/omarchy-nordic-nightfall-theme).

## Requirements

- Omarchy with the `omarchy hook install` command.
- Nordic Nightfall installed under the theme name `nordic-nightfall`.
- The theme's `gtk/gtk-3.0/gtk.css`, `gtk/gtk-4.0/gtk.css`, and
  `icons/Nordic-Nightfall/` assets available in the active theme.
- The `Yaru-blue-dark` icon theme, which the custom folder icons inherit from.
- Bash and `gsettings`. The hook also uses `gtk-update-icon-cache` when available.

## Install

Install Nordic Nightfall first using the theme repository's instructions. Then
clone this repository and install the hook from its separate checkout.

```sh
git clone https://github.com/Z1Z0R/omarchy-nordic-nightfall-theme-hook.git
cd omarchy-nordic-nightfall-theme-hook
omarchy hook install theme-set ./hooks/50-nordic-nightfall-appearance
omarchy theme set nordic-nightfall
```

Omarchy copies the script into
`~/.config/omarchy/hooks/theme-set.d/50-nordic-nightfall-appearance` and makes it
executable. Close and reopen Files after applying or switching themes.

## How it works

On its first run, the hook saves the existing GTK 3 and GTK 4 stylesheets, or
records their absence, under
`~/.local/state/omarchy/nordic-nightfall-appearance/`. This saved baseline is used
on subsequent theme switches.

When `nordic-nightfall` is selected, the hook copies the active theme's GTK
stylesheets into `~/.config/gtk-3.0/gtk.css` and `~/.config/gtk-4.0/gtk.css`.
Their selectors target Files (Nautilus) windows. It also copies the theme's icon
overlay into `~/.local/share/icons/Nordic-Nightfall/` and selects it through
GNOME's icon-theme setting.

When another theme is selected, the hook restores the saved GTK stylesheets.
For a stylesheet that was absent on the first run, it removes the stylesheet
installed by the hook. Omarchy manages the selected theme's icon setting.

## Update

From this repository's checkout, pull the latest version and reinstall the copy
that Omarchy runs.

```sh
git pull --ff-only
omarchy hook install theme-set ./hooks/50-nordic-nightfall-appearance
omarchy theme set nordic-nightfall
```

## Remove

Switch to another theme first so the hook restores the saved GTK stylesheets.
Then remove the installed hook.

```sh
rm ~/.config/omarchy/hooks/theme-set.d/50-nordic-nightfall-appearance
```

Close and reopen Files to load the restored styles.

## License

The hook is provided under the MIT License. See [LICENSE](LICENSE).
