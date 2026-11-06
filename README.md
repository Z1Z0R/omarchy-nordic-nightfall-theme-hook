# Nordic Nightfall appearance hook

An optional Omarchy theme hook that applies Nordic Nightfall's Files colors and
darker blue Yaru folder icons when the theme is selected. This repository contains
the script, GTK stylesheets, and custom icon assets. Install the palette and
wallpapers from the
[Nordic Nightfall theme repository](https://github.com/Z1Z0R/omarchy-nordic-nightfall-theme).

## Requirements

- Omarchy with the `omarchy hook install` command.
- Nordic Nightfall installed under the theme name `nordic-nightfall`.
- This repository's `gtk/` and `icons/` assets installed as described below.
- The `Yaru-blue-dark` icon theme, which the custom folder icons inherit from.
- Bash and `gsettings`. The hook also uses `gtk-update-icon-cache` when available.

## Install

Install Nordic Nightfall first using the theme repository's instructions. Then
clone this repository, copy its assets into the hook's stable data directory,
and install the hook.

```sh
git clone https://github.com/Z1Z0R/omarchy-nordic-nightfall-theme-hook.git
cd omarchy-nordic-nightfall-theme-hook
mkdir -p "$HOME/.local/share/omarchy/nordic-nightfall-appearance"
cp -a ./gtk ./icons "$HOME/.local/share/omarchy/nordic-nightfall-appearance/"
omarchy hook install theme-set ./hooks/50-nordic-nightfall-appearance
omarchy theme set nordic-nightfall
```

Omarchy copies the script into
`~/.config/omarchy/hooks/theme-set.d/50-nordic-nightfall-appearance` and makes it
executable. Close and reopen Files after applying or switching themes.

For an existing installation, these commands replace the installed hook and
install its assets at the new location. The existing GTK restoration baseline
stays in `~/.local/state/omarchy/nordic-nightfall-appearance/`.

## How it works

On its first run, the hook saves the existing GTK 3 and GTK 4 stylesheets, or
records their absence, under
`~/.local/state/omarchy/nordic-nightfall-appearance/`. This saved baseline is used
on subsequent theme switches.

The installed appearance assets live under
`~/.local/share/omarchy/nordic-nightfall-appearance/`. When `nordic-nightfall` is
selected, the hook checks that its GTK stylesheets and icon theme definition
are present before applying them. It copies the GTK stylesheets into
`~/.config/gtk-3.0/gtk.css` and `~/.config/gtk-4.0/gtk.css`. Their selectors target
Files (Nautilus) windows. It also copies the icon overlay into
`~/.local/share/icons/Nordic-Nightfall/` and selects it through GNOME's icon-theme
setting.

When another theme is selected, the hook restores the saved GTK stylesheets.
For a stylesheet that was absent on the first run, it removes the stylesheet
installed by the hook. Omarchy manages the selected theme's icon setting.

## Update

From this repository's checkout, pull the latest version and reinstall the copy
that Omarchy runs.

```sh
git pull --ff-only
mkdir -p "$HOME/.local/share/omarchy/nordic-nightfall-appearance"
cp -a ./gtk ./icons "$HOME/.local/share/omarchy/nordic-nightfall-appearance/"
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

The hook and GTK stylesheets are provided under the MIT License. See
[LICENSE](LICENSE). The adapted Yaru folder icons are licensed under CC BY-SA 4.0.
See [THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md) for attribution and their source.
