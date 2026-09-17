# Data processing 1: Record and ProcessNode

This example prints a Code 128 barcode and its plain text value for each `child` element in the data file, one below the other. It shows how to walk through the XML data with the combination of `<Record>` and `<ProcessNode>`, where each element type has its own `<Record>`. The companion example `dataprocessing2` produces the same output with `<ForAll>`.

## What to look at

- `<SetGrid nx="20" height="12pt" />` divides the page into 20 columns and rows of 12pt.
- `<Record match="root">` contains only `<ProcessNode select="child" />`, which hands each `child` element to the matching `<Record match="child">`.
- `<Record match="child">` places an `<HTML expand-text="yes">` block. With `expand-text="yes"` the curly braces in `value="{.}"` and in the paragraph are evaluated as XPath expressions, so the text of the current `child` element appears both in the barcode and below it.
- `<barcode type="code128" value="{.}" width="5cm" height="1.5cm" />` inside the HTML block creates the barcode.
- `<NextRow rows="2" />` after each object moves the cursor down by two grid rows, so the entries do not touch.

## Run

Run `xts` in this directory. The result is `xts.pdf`; `result.pdf` is the expected output for comparison.

![First page](firstpage.png)
