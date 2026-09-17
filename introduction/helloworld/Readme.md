# Hello, world

The smallest possible XTS document: the text `Hello, world!` from the data file is placed on a page. This example shows the minimal chain from data to PDF, a `<Record>` that matches the root element, a `<PlaceObject>` and a `<TextBlock>` with one `<Paragraph>`.

## What to look at

- `<Record match="data">` is entered for the root element `data` of `data.xml`.
- `<PlaceObject>` without `column` or `row` places the object at the current position of the page (the top left of the page area).
- `<TextBlock>` and `<Paragraph>` wrap the text.
- `<Value select="."/>` inserts the text content of the current node, here the string `Hello, world!`.

## Run

Run `xts` in this directory. The result is `xts.pdf`; `result.pdf` is the expected output for comparison.

![First page](firstpage.png)
