# Japanese LaTeX Classes

There are a number of classes to choose from. The most relevant ones are the *j* and *js* class families, as well as the `jlreq` class.

## General Information

### Summary

The *j* classes have a number of flaws which make them less than ideal for typesetting professional documents. The *js* classes addressed these issues, effectively rendering their *j* class counterparts obsolete.

Another good option is the `jlreq` class. As there are no vertical *js* classes, it is the *only* option for producing high quality vertical documents without manually tweaking settings.

In short:

- *j* classes should be avoided, unless you know what you're doing.
- *js* classes just work, *if* you're writing *horizontal documents*.
- `jlreq` just works.

The recommendation is therefore to simply stick with `jlreq` for a unified experience, although the *js* classes are perfectly acceptable as well.

### A note on font switching

The *js* classes and `jlreq` automatically synchronize Latin and Japanese font families. This means that switching between *roman/sans* fonts (`\rmfamily`/`\sffamily`) will automatically switch the Japanese family to *mincho/gothic* (`\mcfamily`/`\gtfamily`).

This behavior can be replicated in other classes by loading the `minijs` package in (u)pLaTeX, and by giving the `match` option to `luatexja-fontspec` or`luatexja-preset` in LuaLaTeX.

### Common options

The `twocolumn` option is used to split the text being typeset into two columns. It's particularly useful for reducing the line length of a document when text is being typeset along the long edge of a large paper.

As an example, compare the results of typesetting [`wagahai.tex`](../examples/wagahai.tex) (a vertical document, typeset on A4-sized paper in portrait orientation):

- with `twocolumn`: [`wagahai_twocolumn.pdf`](../examples/wagahai_twocolumn.pdf)
- without `twocolumn`: [`wagahai_onecolumn.pdf`](../examples/wagahai_onecolumn.pdf)

### Class-defined macros

Like packages, classes can also define user-level macros. One example is of this is the `\和暦`/`\西暦` macro pair, which are defined by all Japanese classes. When called, they change the output of the `\today` command.

The following example,

```latex
\documentclass{jsarticle}
\和暦
\begin{document}
\today

\西暦
\today
\end{document}
```

when compiled on 2022-08-09, produces:

![](../imt/../img/wareki.png)

## List of classes

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

Note that `jlreq` sets the papersize using `paper=a4`, as opposed to most other classes which use `a4paper`.

### Other classes

For some document types, there are no Japanese variants available. An example of this is the `beamer` class, which is used for creating presentations.

As non-Japanese document classes do not load their own font metrics, the default metrics of the compiling engine will be used in these cases. This can be problematic if using pLaTeX, as there a number of problems with its default font metrics.

In these cases, loading the `minijs` and/or `otf` packages will replace the font metric with one based on the *jis* font metric.

- See the [packages](./packages.md) article for information about these packages.
- See [this](../advanced/jsclasses.md) post for more information about the problems with the default pLaTeX font metric.

## Resources

- [【LaTeX】用紙サイズ・向きの設定方法](https://mathlandscape.com/latex-papersize/)
  - Japanese post about configuring paper size in different document classes.
