# Simple table

This example creates a two column price table with a header row and one row per `entry` element from the data file. It shows the basic table elements `<Table>`, `<Tr>` and `<Td>`, a loop over data rows and CSS for table width and cell alignment.

## What to look at

- `<StyleSheet>` sets `table { width: 100% }` and `td.right { text-align: right }`.
- `<Table width="5">` gives the table a width of five grid cells; the `width: 100%` rule makes the table use this width.
- The first `<Tr>` is written out in the layout and serves as the header row with the texts `Article number` and `Price (Euro)`.
- `<ForAll select="entry">` creates one `<Tr>` per `entry` element with `<Value select="@artno" />` and `<Value select="@price" />`.
- `<Td class="right">` applies the CSS class so that the price column is right aligned.

## Run

Run `xts` in this directory. The result is `xts.pdf`; `result.pdf` is the expected output for comparison.

![First page](firstpage.png)
