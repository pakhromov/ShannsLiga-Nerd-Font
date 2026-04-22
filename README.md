# Shanns Liga Nerd Fonts

This collection of fonts is a combination of [ComicShannsMono Nerd Font](https://github.com/ryanoasis/nerd-fonts/tree/master/patched-fonts/ComicShannsMono) and [SeriousShanns Nerd Font](https://github.com/kaBeech/serious-shanns) with ligatures from [RecMonoSmCasual Nerd Font](https://github.com/ryanoasis/nerd-fonts/tree/master/patched-fonts/Recursive).

## Variations

There are 3 variations for both ComicShanns and SeriousShanns:

### 1. LigaPure - The original fonts with only ligatures added and nothing else changed.

`ComicShannsLigaPure Nerd Font`

![ComicShannsLigaPure Nerd Font](meta/ComicShannsLigaPure%20Nerd%20Font.png)

`SeriousShannsLigaPure Nerd Font`

![SeriousShannsLigaPure Nerd Font](meta/SeriousShannsLigaPure%20Nerd%20Font.png)

### 2. Liga - Same as Pure, but the following characters are replaced with their RecMonoSmCasual equivalents to make it have a consistent look with ligatures:



`< > / | \ = - + _ #`

`ComicShannsLiga Nerd Font`

![ComicShannsLiga Nerd Font](meta/ComicShannsLiga%20Nerd%20Font.png)

`SeriousShannsLiga Nerd Font`

![SeriousShannsLiga Nerd Font](meta/SeriousShannsLiga%20Nerd%20Font.png)

### 3. LigaMod - Same as Liga, with additional opinionated replacements from RecMonoSmCasual that I personally like more

`0 1 2 3 4 5 6 7 8 9 $ ( ) [ ] { }`

So the full set of replaced characters is:

`< > / | \ = - + _ # 0 1 2 3 4 5 6 7 8 9 $ ( ) [ ] { }`

`ComicShannsLigaMod Nerd Font`

![ComicShannsLigaMod Nerd Font](meta/ComicShannsLigaMod%20Nerd%20Font.png)

`SeriousShannsLigaMod Nerd Font`

![SeriousShannsLigaMod Nerd Font](meta/SeriousShannsLigaMod%20Nerd%20Font.png)

## Building from source

The fonts are generated using two Python scripts that require [fonttools](https://github.com/fonttools/fonttools):

```
pip install fonttools
```

- **`ligaturize_ft.py`** - copies the CALT ligature table and ligature glyphs from a source font into a target font
- **`modchars_ft.py`** - replaces specific character glyphs in a font with ones from a donor font

### Usage

```bash
python3 ligaturize_ft.py <target_font> <source_font> <output_file> <family_name>

python3 modchars_ft.py <target_font> <donor_font> <output_file> <family_name> [mod|mod2]
```

### Generating all variants

Set up variables:

```bash
COMIC=/path/to/ComicShannsMonoNerdFont
SERIOUS=/path/to/SeriousShannsNerdFont
RECS=/path/to/RecMonoSmCasualNerdFont
OUT=output
mkdir -p $OUT
```

**Step 1 - Pure:**
```bash
for style in Regular Bold; do
    python3 ligaturize_ft.py ${COMIC}-${style}.otf   ${RECS}-${style}.ttf ${OUT}/ComicShannsLigaPureNerdFont-${style}.otf   "ComicShannsLigaPure Nerd Font"
done
for style in Regular Bold Italic BoldItalic; do
    python3 ligaturize_ft.py ${SERIOUS}-${style}.otf ${RECS}-${style}.ttf ${OUT}/SeriousShannsLigaPureNerdFont-${style}.otf  "SeriousShannsLigaPure Nerd Font"
done
python3 ligaturize_ft.py ${SERIOUS}-Light.otf       ${RECS}-Regular.ttf ${OUT}/SeriousShannsLigaPureNerdFont-Light.otf       "SeriousShannsLigaPure Nerd Font"
python3 ligaturize_ft.py ${SERIOUS}-LightItalic.otf ${RECS}-Italic.ttf  ${OUT}/SeriousShannsLigaPureNerdFont-LightItalic.otf  "SeriousShannsLigaPure Nerd Font"
```

**Step 2 - Liga:**
```bash
for style in Regular Bold; do
    python3 modchars_ft.py ${OUT}/ComicShannsLigaPureNerdFont-${style}.otf  ${RECS}-${style}.ttf ${OUT}/ComicShannsLigaNerdFont-${style}.otf   "ComicShannsLiga Nerd Font" mod
done
for style in Regular Bold Italic BoldItalic; do
    python3 modchars_ft.py ${OUT}/SeriousShannsLigaPureNerdFont-${style}.otf ${RECS}-${style}.ttf ${OUT}/SeriousShannsLigaNerdFont-${style}.otf  "SeriousShannsLiga Nerd Font" mod
done
python3 modchars_ft.py ${OUT}/SeriousShannsLigaPureNerdFont-Light.otf       ${RECS}-Regular.ttf ${OUT}/SeriousShannsLigaNerdFont-Light.otf       "SeriousShannsLiga Nerd Font" mod
python3 modchars_ft.py ${OUT}/SeriousShannsLigaPureNerdFont-LightItalic.otf ${RECS}-Italic.ttf  ${OUT}/SeriousShannsLigaNerdFont-LightItalic.otf  "SeriousShannsLiga Nerd Font" mod
```

**Step 3 - LigaMod:**
```bash
for style in Regular Bold; do
    python3 modchars_ft.py ${OUT}/ComicShannsLigaPureNerdFont-${style}.otf  ${RECS}-${style}.ttf ${OUT}/ComicShannsLigaModNerdFont-${style}.otf   "ComicShannsLigaMod Nerd Font" mod2
done
for style in Regular Bold Italic BoldItalic; do
    python3 modchars_ft.py ${OUT}/SeriousShannsLigaPureNerdFont-${style}.otf ${RECS}-${style}.ttf ${OUT}/SeriousShannsLigaModNerdFont-${style}.otf  "SeriousShannsLigaMod Nerd Font" mod2
done
python3 modchars_ft.py ${OUT}/SeriousShannsLigaPureNerdFont-Light.otf       ${RECS}-Regular.ttf ${OUT}/SeriousShannsLigaModNerdFont-Light.otf       "SeriousShannsLigaMod Nerd Font" mod2
python3 modchars_ft.py ${OUT}/SeriousShannsLigaPureNerdFont-LightItalic.otf ${RECS}-Italic.ttf  ${OUT}/SeriousShannsLigaModNerdFont-LightItalic.otf  "SeriousShannsLigaMod Nerd Font" mod2
```

## Credits

- [ComicShannsMono](https://github.com/shannpersand/comic-shanns) by Shannon Miwa
- [SeriousShanns](https://github.com/kaBeech/serious-shanns) by Kyle Beechly
- [Recursive / RecMonoSmCasual](https://www.recursive.design/) by Arrow Type
- [Nerd Fonts](https://www.nerdfonts.com/) patching by Ryan L McIntyre
