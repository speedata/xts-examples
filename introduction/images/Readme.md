# Images

This example places eight images of different types (PDF pages, JPEG, PNG, a generated placeholder and one file that does not exist) below each other in the first column of the page. It shows the `<Image>` element with a fixed height in grid cells, the `placeholder://` scheme and how the `imagenotfound` option controls what happens with a missing image file.

## What to look at

- `<Options imagenotfound="warning" />` makes a missing image file a warning: a placeholder is used instead and processing continues.
- `<Image href="ocean.pdf" height="3" />`, `oceancrop.pdf`, `yellowblue.jpg`, `img.png`, `gradient.png` and `268385.png` are placed with `<PlaceObject column="1">` and `height="3"`, three grid rows each. Without `row`, each object is placed below the previous one.
- `<Image href="placeholder://600x400" height="3" />` uses the `placeholder://` scheme to create a placeholder image with the given pixel size instead of loading a file.
- `<Image href="doesnotexist.pdf" height="3" width="2" />` refers to a file that is not in the directory. Together with `imagenotfound="warning"` this results in a placeholder of the given size and a warning in the protocol file.

## Run

Run `xts` in this directory. The result is `xts.pdf`; `result.pdf` is the expected output for comparison.

No data file is needed because `xts.cfg` sets `dummy=true` and the layout does not read any data.

![First page](firstpage.png)
