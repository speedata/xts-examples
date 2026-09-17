# Text formatting

This example shows four ways to get formatted text (italic, bold, bulleted lists) into a document: HTML in a CDATA section of the data file, XML markup in the data file, XTS elements in the layout file and XHTML elements in the layout file. All four produce the same paragraph and list, so you can compare the approaches side by side.

## What to look at

- `<SetGrid height="14pt" width="1cm" />` and a `<StyleSheet>` that sets `body` to 14pt serif, a `.title` class and an `@font-face` for `code` with `src: local("CamingoCode Regular")` and `size-adjust: 80%`.
- `<HTML select="html" />` reads the HTML fragment from the CDATA section of the `html` element in `data.xml` and renders it.
- `<CopyOf select="text" />` inside a `<Paragraph>` copies the child nodes of the `text` element, including its `<i>`, `<b>` and `<ul>` markup, from the data file.
- `<I>`, `<B>`, `<Ul>` and `<Li>` are the XTS layout elements for the same formatting written directly in the layout.
- `<HTML>` with XHTML elements in the `h:` namespace (`xmlns:h="http://www.w3.org/1999/xhtml"`) such as `<h:i>`, `<h:b>`, `<h:ul>` and `<h:li>` is the fourth variant.
- The line `&amp; # \ { } %` in each variant shows that characters with a special meaning in other typesetting systems need no escaping here.

## Run

Run `xts` in this directory. The result is `xts.pdf`; `result.pdf` is the expected output for comparison.

![First page](firstpage.png)
