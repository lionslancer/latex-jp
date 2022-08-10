# Japanese typesetting with LaTeX

This repository contains useful information for getting started with typesetting Japanese documents in LaTeX.

## Table of Contents

### Basic Topics

- [Japanese TeX Engines](guide/engines.md)
  - Summarizes the three main engines available for typesetting Japanese.
- [Japanese LaTeX Classes](guide/classes.md)
  - Summarizes the main classes used for typesetting Japanese.
- [Japanese LaTeX Packages](guide/packages.md)
  - Lists commonly used packages and which engines they are compatible with.
- [Using Japanese counter styles in enumerated lists](guide/enumeration.md)
  - Explains how to use Japanese counter styles like いろは in enumerated lists.

### Advanced Topics

- [*js* classes and the *jis* font metric](advanced/jsclasses.md)
  - Explains the differences between the *j* classes and *js* classes, as well as the *jis* font metric. Read the main guide first.
- [Whitespace and linebreaks](advanced/linebreak.md)
  - In-depth explanation of how whitespace and line breaks are handled in Japanese documents, and how 禁則処理 (line breaking rules) are implemented.

## tl;dr: Use `jlreq` with LuaTeX

### Key points

Here is a summary of the most important points:

- The `jlreq` class does pretty much everything you need:
  - based on [JLREQ](https://www.w3.org/TR/jlreq/) (the W3C specification for Japanese text layout).
  - takes document types (`article`, `book`, `report`) as options.
- Use the `luatexja-preset` package with the `deluxe` option to enable multiple font weights.
- Use the `pxrubrica` package to typeset furigana and kenten.

### Example

The following example[^1] will output the beginning of "I am a cat" by Natsume Soseki, typeset vertically:

```latex
\documentclass[a4paper, book, tate, twocolumn]{jlreq}
\usepackage{bxjalipsum}
\begin{document}
\title{吾輩は猫である}% I Am A Cat
\author{夏目漱石}% Natsume Soseki
\maketitle
\jalipsum{wagahai}% 吾輩は猫である。名前... (33 paragraphs)
\end{document}
```

The output can be seen [here](examples/wagahai_twocolumn.pdf).

[^1]: Slightly modified version of an example from *Guide to Japanese typesetting with LaTeX*.

## Resources

Sources for the information in this repository, and other useful links. If using TeX Live, some of these documents can be read using `texdoc`.

### Guides in English

- [*Guide to Japanese typesetting with LaTeX*](http://mirrors.ctan.org/macros/latex/contrib/babel-contrib/japanese/japanese.pdf)
  - `texdoc japanese`
- Overleaf [Japanese](https://www.overleaf.com/learn/latex/Japanese) guide
- [How to write Japanese with LaTeX?](https://tex.stackexchange.com/questions/15516/how-to-write-japanese-with-latex) on TeX StackExchange

### Guides in Japanese

- [日本語 LaTeX の新常識 2021](https://qiita.com/wtsnjp/items/76557b1598445a1fc9da)
- [TeX Live ドキュメント案内](https://qiita.com/wtsnjp/items/f8d853cccb9fd95b012c)
  - Long list of documents related to Japanese LaTeX
- Japanese [TeX Wiki](https://texwiki.texjp.org/)

### Journal articles on Japanese typesetting

- Haruhiko Okumura, [*"pTeX and Japanese Typesetting"*](http://ajt.ktug.org/2008/0201okumura.pdf), The Asian Journal of TeX, Volume 2, No. 1, 2008.
- Hironori Kitagawa, [*"Development of the LuaTEX-ja package"*](http://ajt.ktug.org/2011/0502kitagawa.pdf), The Asian Journal of TeX, Volume 5, No. 2, 2011.

### Package documentation

- [*The LuaTEX-ja package*](http://mirrors.ctan.org/macros/luatex/generic/luatexja/doc/luatexja-en.pdf)
  - `texdoc luatexja`

### Standards

- [*Requirements for Japanese Text Layout*](http://www.w3.org/TR/jlreq/)
