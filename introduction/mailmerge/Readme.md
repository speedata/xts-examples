# Mail merge

This example produces a form letter for every `record` element in the data file, one US Letter page per addressee. It shows a master page with a company header and logo, named positioning areas for the recipient block and the company block, an external CSS file and `<ClearPage/>` to start a new page after each letter.

## What to look at

- `<PageFormat width="8.5in" height="11in"/>` and `<SetGrid height="12pt" nx="30"/>` set up a US Letter page with a 30 column grid.
- `<StyleSheet href="style.css" />` loads the `.company` class (8pt sans, right aligned) from an external file.
- `<DefineMasterPage name="page" test="true()" margin="10mm 10mm 10mm 10mm">` applies to every page. It defines two `<PositioningArea>` elements, `recipient` and `company`, each with a `<PositioningFrame>` at a fixed grid position.
- `<AtPageCreation>` places `logo.pdf` and the company address (`<Paragraph class="company">`, with `<A href="...">` for the web link) in the `company` area on every new page.
- `<Record match="root">` uses `<ProcessNode select="record"/>`, and `<Record match="record">` typesets one letter: the address in `area="recipient"`, the date at `row="20" column="1"`, and the body with `<Value select="concat(@first_name,' ',@last_name,',')"/>` for the salutation.
- `<ClearPage/>` at the end of each `record` starts the next letter on a new page.
- `<Trace grid="no" gridallocation="no">` is present but switched off; set it to `yes` to see the grid and the allocated cells.

## Run

Run `xts` in this directory. The result is `xts.pdf`; `result.pdf` is the expected output for comparison.

![First page](firstpage.png)
