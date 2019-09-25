Do you experience black/white emojis or only boxes when someone sends you an emoji on Linux?

**Wire-Desktop** is using system fonts for emojis. This means that if you fix your system emoji, not only they will be beautiful on Wire, they will be beautiful in every other app you have (that also uses system emoji).

**Here is how to fix them:**

1. Get [EmojiOne](https://emojione.com) font from [their GitHub repository](https://github.com/emojione/emojione/tree/master/extras/fonts). You can use the Android .ttf to get colored emojis or try the .otf or .woff versions for black and white emojis.

2. Install the new font (through applications like "Gnome Font Viewer" or by directly copying the TTF to `~/.local/share/fonts/`)

3. Prioritize the emoji font over other fonts (especially Symbola) by creating the file `~/.config/fontconfig/conf.d/70-emojione-color.conf` and add the following content:

```html
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>

  <!-- Add emoji generic family -->
  <alias binding="strong">
    <family>emoji</family>
    <default><family>Emoji One</family></default>
  </alias>

  <!-- Aliases for the other emoji fonts -->
  <alias binding="strong">
    <family>Apple Color Emoji</family>
    <prefer><family>Emoji One</family></prefer>
  </alias>
  <alias binding="strong">
    <family>Segoe UI Emoji</family>
    <prefer><family>Emoji One</family></prefer>
  </alias>
  <alias binding="strong">
    <family>Noto Color Emoji</family>
    <prefer><family>Emoji One</family></prefer>
  </alias>

  <!-- Do not allow any app to use Symbola, ever -->
  <selectfont>
    <rejectfont>
      <pattern>
        <patelt name="family">
          <string>Symbola</string>
        </patelt>
      </pattern>
    </rejectfont>
  </selectfont>
</fontconfig>
```

4. Run `fc-cache -f` to rebuild the font cache after you change your font configuration

(Thanks to @maximbaz for this instructions)

**You can run the steps from above with the following script:**

```sh
#!/usr/bin/env bash

# Script for instructions at this page:
# https://github.com/wireapp/wire-desktop/wiki/Colorful-emojis-on-Linux

set -e
set -o pipefail

tmp=$(mktemp)
curl -sSLf https://github.com/emojione/emojione-assets/releases/download/4.5/emojione-android.ttf > "$tmp"

#fail script if sha256sum mismatch
echo "checking sha..."
sha256=5a8ec97548326235f427dff60749bdbd525de20383c42b1ae73f3bae883f58c2
echo "$sha256 $tmp" | sha256sum --check --status
echo "sha valid"

mkdir -p ~/.local/share/fonts/
mv "$tmp" ~/.local/share/fonts/emojione-android.ttf

echo "writing font config..."
mkdir -p ~/.config/fontconfig/conf.d
echo '<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>

  <!-- Add emoji generic family -->
  <alias binding="strong">
    <family>emoji</family>
    <default><family>Emoji One</family></default>
  </alias>

  <!-- Aliases for the other emoji fonts -->
  <alias binding="strong">
    <family>Apple Color Emoji</family>
    <prefer><family>Emoji One</family></prefer>
  </alias>
  <alias binding="strong">
    <family>Segoe UI Emoji</family>
    <prefer><family>Emoji One</family></prefer>
  </alias>
  <alias binding="strong">
    <family>Noto Color Emoji</family>
    <prefer><family>Emoji One</family></prefer>
  </alias>

  <!-- Do not allow any app to use Symbola, ever -->
  <selectfont>
    <rejectfont>
      <pattern>
        <patelt name="family">
          <string>Symbola</string>
        </patelt>
      </pattern>
    </rejectfont>
  </selectfont>
</fontconfig>
' > ~/.config/fontconfig/conf.d/70-emojione-color.conf

fc-cache -f

echo "done."
```

(Thanks to @jschaul for the script)