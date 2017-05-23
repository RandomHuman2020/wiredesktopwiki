Do you experience black/white emojis or only boxes when someone sends you an emoji on Linux?

**Wire-Desktop** is using system fonts for emojis. This means that if you fix your system emoji, not only they will be beautiful on Wire, they will be beautiful in every other app you have (that also uses system emoji).

**Here is how to fix them:**

1. Get [EmojiOne](https://emojione.com) font for Android from [their GitHub repository](https://github.com/Ranks/emojione/blob/master/extras/fonts/emojione-android.ttf)

2. Install the new font (through applications like "Gnome Font Viewer" or by directly copying the TTF to `~/.local/share/fonts/`)

3. Prioritize the emoji font over other fonts (especially Symbola) by creating the file `~/.config/fontconfig/conf.d/70-emojione-color.conf` and add the following content:

```
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