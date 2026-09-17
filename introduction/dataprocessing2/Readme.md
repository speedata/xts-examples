# Data processing 2: ForAll

This example produces the same document as `dataprocessing1`, a Code 128 barcode plus its text for each `child` element, but it iterates over the elements with `<ForAll>` inside a single `<Record>` instead of dispatching to a second `<Record>` with `<ProcessNode>`. It also shows a layout function call inside an attribute value.

## What to look at

- `<SetGrid nx="20" height="12pt" />` sets a 20 column grid with 12pt rows.
- `<Record match="root">` contains `<ForAll select="child">`, which repeats its content for every `child` element. The current node inside the loop is the `child` element.
- `<HTML expand-text="yes">` evaluates the curly brace expressions, `{.}` for the text of the current element.
- `width="{sd:grid-width(5,'cm')}cm"` on the `<barcode>` element calls the layout function `sd:grid-width()` to compute the width of five grid cells in centimetres.
- `<NextRow rows="2" />` moves down two grid rows after each entry.

## Run

Run `xts` in this directory. The result is `xts.pdf`; `result.pdf` is the expected output for comparison.

![First page](firstpage.png)
