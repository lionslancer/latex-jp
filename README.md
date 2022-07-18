# Japanese typesetting with LaTeX

This repo contains useful information for getting started with typesetting Japanese documents in LaTeX.

## Table of Contents

- [Primer on writing Japanese documents with LaTeX](guide)
  - The main guide. Summarizes the various engines, classes, and packages that are available.

- [*js* classes and the *jis* font metric](jsclasses)
  - Explains the differences between the *j* classes and *js* classes, as well as the *jis* font metric. Read the main guide first.

- [Whitespace and linebreaks](linebreak)
  - More in-depth explanation of how whitespace and line breaks are handled in Japanese documents, and how 禁則処理 (line breaking rules) are implemented.

- [Using Japanese counter styles in enumerated lists](enumeration)
  - Explains how to customize lists to use Japanese counter styles such as いろは.

## tl;dr: Use `jlreq` with `LuaTeX`

- The `jlreq` class does pretty much everything you need:
  - based on [JLREQ](https://www.w3.org/TR/jlreq/) (the W3C specification for Japanese text layout).
  - takes document types (`article`, `book`, `report`) as options.

- Use the `luatexja-preset` package with the `deluxe` option to enable multiple font weights.
  - also used to change the font, but the default happens to be one of the best fonts available.

- Use the `pxrubrica` package to typeset furigana and kenten.

The following example[^1] will output the beginning of "I am a cat" by Natsume Soseki, typeset vertically in landscape format:

```latex
\documentclass[a4paper, book, tate, landscape]{jlreq}
\usepackage{bxjalipsum}
\begin{document}
\title{吾輩は猫である}% I Am A Cat
\author{夏目漱石}% Natsume Soseki
\maketitle
\jalipsum{wagahai}% 吾輩は猫である。名前... (33 paragraphs)
\end{document}
```

See [`wagahai.pdf`](wagahai.pdf) for the output.

[^1]: Slightly modified version of an example from *Guide to Japanese typesetting with LaTeX*.

## See also

Sources for the information in this repository, and other useful links.

Other guides:

- [*Guide to Japanese typesetting with LaTeX*](http://mirrors.ctan.org/macros/latex/contrib/babel-contrib/japanese/japanese.pdf)
- Overleaf [Japanese](https://www.overleaf.com/learn/latex/Japanese) guide

Journal articles on Japanese typesetting:

- Haruhiko Okumura, [*"pTeX and Japanese Typesetting"*](http://ajt.ktug.org/2008/0201okumura.pdf), The Asian Journal of TeX, Volume 2, No. 1, 2008.
- Hironori Kitagawa, [*"Development of the LuaTEX-ja package"*](http://ajt.ktug.org/2011/0502kitagawa.pdf), The Asian Journal of TeX, Volume 5, No. 2, 2011.

Package documentation:

- [*The LuaTEX-ja package*](http://mirrors.ctan.org/macros/luatex/generic/luatexja/doc/luatexja-en.pdf)

Standards:

- [*Requirements for Japanese Text Layout*](http://www.w3.org/TR/jlreq/)
