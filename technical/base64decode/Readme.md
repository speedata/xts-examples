# Base64 decoded image

This example places an image whose PNG data is stored base64 encoded directly in the data file instead of as a separate file. It shows how to decode the data with layout functions and hand the result to `<Image>`.

## What to look at

- `data.xml` contains only the base64 encoded bytes of a PNG file as the text of the `data` element.
- `sd:decode-base64(.)` decodes the text of the current node into binary data.
- `sd:file-contents(...)` wraps this data so that it can be used as an image source.
- `<Image href="{sd:file-contents(sd:decode-base64(.))}">` places the decoded image; the `href` attribute is an XPath expression in curly braces.

## Run

Run `xts` in this directory. The result is `xts.pdf`; `result.pdf` is the expected output for comparison.

![First page](firstpage.png)
