# Primer on writing Japanese documents with LaTeX

## Engines

### About the engines

There are three main engines available for typesetting Japanese documents:

- *pTeX* is a TeX engine designed for typesetting Japanese. It uses special mechanisms to support the conventions of Japanese typesetting, which cannot be provided through a normal package.

- *upTeX* is the unicode version of pTeX. Its existence effectively makes pTeX obselete, other than for legacy purposes. pTeX seems to be able to handle files encoded in UTF-8 these days, but unlike upTeX, it will fail if the input contains characters that did not exist in its original encoding.

- The `luatexja` package implements pTeX primitives in the LuaTeX engine. This is possible through the use of Lua callbacks, enabling the implementation of features which cannot be built with TeX primitives alone.

upTeX and LuaTeX each have their own strengths. upTeX uses the pLaTeX2ε format, while LuaTeX uses the more common LaTeX2ε format. This means that some packages written for pTeX will refuse to work with LuaTeX, and vice versa. LuaTeX is more compatible with modern packages, with many specifically taking advantage of LuaTeX's built-in Lua interpreter.

I would recommend sticking with LuaTeX unless a (u)pTeX-specific package is required. LuaTeX is the future, and `luatexja` is  mature enough to be the default choice.

### Compilation

If using (u)pTeX, the `plautopatch` package should be loaded at the beginning of the document, in order to automatically resolve incompatibilites between (u)pTeX and certain Western LaTeX packages.

Additionally, because (u)pTeX outputs to DVI, it is good to specify the DVI driver as a package option. If an option such as `landscape` is passed to the document class, the DVI driver will not automatically detect that the dimensions have been changed. When a paper size option is used, loading the `bxpapersize` package will ensure that the DVI driver uses the correct dimensions.

For pTeX:

```latex
\RequirePackage{plautopatch}
\documentclass[dvipdfmx]{jsarticle}
```

For upTeX (landscape document):

```latex
\RequirePackage{plautopatch}
\documentclass[uplatex, dvipdfmx]{jsarticle}
\usepackage{bxpapersize}
```

Note: `\RequirePackage` is used in order load a package before the document class.

Compile as follows (remove the initial 'u' if using pTeX):

```shell
uplatex -kanji=utf8 -no-guess-input-enc
dvipdfmx file.dvi
```

The flags are used to ensure that the input is interpreted as being UTF-8. By default, (u)pTeX will attempt to guess the encoding, with varying success. More information available [here](https://texwiki.texjp.org/?upTeX%2CupLaTeX#rfce644f) (in Japanese).

LuaTeX documents are compiled with:

```shell
lualatex file.tex
```

## Classes

There are a number of classes to choose from. The most relevant ones are the *j* and *js* class families, as well as the `jlreq` class.

### *j* classes

The *j* classes are the default pLaTeX classes.

- Horizontal classes are prefixed with *j*:
  - upLaTeX variants are prefixed with *uj*.
  - LuaLaTeX variants are prefixed with *ltj*.

  Type    | pLaTeX   | upLaTeX   | LuaLaTeX   |
  --------|----------|-----------|------------|
  Article |`jarticle`|`ujarticle`|`ltjarticle`|
  Book    |`jbook`   |`ujbook`   |`ltjbook`   |
  Report  |`jreport` |`ujreport` |`ltjreport` |

- Vertical classes are prefixed with *t*:
  - upLaTeX variants are prefixed with *ut*.
  - LuaLaTeX variants are prefixed with *ltjt*.

  Type    | pLaTeX   | upLaTeX   | LuaLaTeX    |
  --------|----------|-----------|-------------|
  Article |`tarticle`|`utarticle`|`ltjtarticle`|
  Book    |`tbook`   |`utbook`   |`ltjtbook`   |
  Report  |`treport` |`utreport` |`ltjtreport` |

### *js* classes

The *js* classes are improved versions of the *j* classes, created by Haruhiko Okumura. They were designed to be compliant with JIS X 4051 (the JIS standard for typesetting). Unfortunately, only horizontal classes are available.

- Classes are prefixed with *js*:
  - There are no upLaTeX variants; use the regular variant with option `uplatex`.
  - LuaLaTeX variants are prefixed with *ltjs*.

  Type    | pTeX      | upTeX     | LuaTeX      |
  --------|-----------|-----------|-------------|
  Article |`jsarticle`|`jsarticle`|`ltjsarticle`|
  Book    |`jsbook`   |`jsbook`   |`ltjsbook`   |
  Report  |`jsreport` |`jsreport` |`ltjsreport` |

### `jlreq`

`jlreq` is a single class, designed to implement [Requirements for Japanese Text Layout](https://www.w3.org/TR/jlreq/) (aka JLREQ), the W3C specification for Japanese text layout. This document is largely based on JIS X 4051, so the two should not be in conflict.

 `jlreq` uses options to fullfill multiple roles with a single class:

- Engine: `platex`, `uplatex`, `lualatex`.
- Document type: `article`, `book`, `report`.
- Direction: `yoko`, `tate`.

### Comments

The *j* classes have a number of flaws which make them less than ideal for professional documents. The *js* classes addressed these issues, effectively rendering their *j* class counterparts obsolete.

The second good option is the `jlreq` class. As there are no vertical *js* classes, it is the *only* option for producing high quality vertical documents without manually tweaking settings.

In short:

- *j* classes should be avoided, unless you know what you're doing.
- *js* classes just work, *if* you're writing *horizontal documents*.
- `jlreq` just works.

The recommendation is therefore to simply stick with `jlreq` for a unified experience, although the *js* classes are perfectly acceptable as well.

## Packages

Suggested packages for commonly used features.

### Furigana and Kenten

Packages for entering ruby text (furigana). Also provide macros for typesetting emphasis dots (kenten).

LuaLaTeX:

- `pxrubrica`
  - Compliant with JLREQ and JIS X 4051. Typesets horizontal kenten using "•",  and vertical kenten using "﹅", as [suggested](https://www.w3.org/TR/jlreq/#composition_of_emphasis_dots) by JLREQ.
- `luatexja-ruby`
  - Uses Lua callbacks. Always uses "•" to typeset kenten, regardless of direction. Included here for the sake of completeness; `pxrubrica` is recommended.

(u)pLaTeX:

- `pxrubrica`
  - Compliant with JLREQ and JIS X 4051.

### Multiple font weights

By default, only two fonts are available: a regular-weight *mincho* font and a bold *gothic* font. That means switching to a bold font will automatically switch to *gothic* and vice versa. Using one of these packages will enable bold *mincho*, etc.

LuaLaTeX:

- `luatexja-fontspec` w/ `deluxe` option
  - Use this if selecting the font using `luatexja-fontspec`.
- `luatexja-preset` w/ `deluxe` option
  - Use this if selecting the font using `luatexja-preset`.

(u)pLaTeX:

- `jlreq-deluxe`
  - Use this if using the `jlreq` class. `jlreq` uses a custom font metric which will be overwritten if the `otf` package is loaded.
- `otf` w/ `deluxe` option
  - Standard choice for (u)pLaTeX.

### Font selection

Used to change which fonts will be used in the final document. This is independent of which weights are available.

LuaLaTeX:

- `luatexja-fontspec`
  - Used to configure custom fonts for use with Japanese.
- `luatexja-preset`
  - Provides presets for popular fonts. Loads `luatexja-fontspec` internally.

(u)pLaTeX:

- `pxchfon`
  - Used to configure custom fonts. Also provides presets for popular fonts.

### Unicode/CID input

These packages enable inputting characters using the Unicode code point or Adobe CID. For the character ㋿, that would be `\UTF{32FF}` and `\CID{23058}`.

LuaLaTeX:

- `luatexja-otf`
  - Only used for providing these features, as weights are managed by `luatexja-fontspec`.

(u)pLaTeX:

- `jlreq-deluxe`
  - Use this if using the `jlreq` class. Use option `deluxe=false` if you only want the input commands and don't need multiple weights.
- `otf`
  - Standard choice for (u)pLaTeX.

### Dummy Text/Lorem Ipsum

Packages for typesetting lipsum text.

- `bxjalipsum`
  - Compatible with all engines.
