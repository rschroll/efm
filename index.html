<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8" />
<title>EFM &mdash; Epub for Monocle</title>
<!--
Copyright (c) 2010 Joseph Pearson
Copyright (c) 2013 Robert Schroll

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
-->
<script src="js/zip.js"></script>
<script src="js/monocore.js"></script>
<script src="js/monoctrl.js"></script>
<script src="efm.js"></script>
<script type="text/javascript" charset="utf-8">
// This is some basic code for using Monocle with EFM.
// First, we need to tell zip.js where to find its accessory files.
zip.workerScriptsPath = "js/"

// An event handler for our file input.
function fileSelected(event) {
    var files = event.target.files;
    if (files.length > 0)
        new Epub(files[0], createReader);
}

// This will be called when the Epub object is fully initialized and
// ready to get passed to the Monocle.Reader.
function createReader(bookData) {
    Monocle.Reader("reader", bookData,  // The id of the reader element and the book data.
        { flipper: Monocle.Flippers.Instant,  // The rest is just fanciness:
          panels: Monocle.Panels.Magic },     // No animation and click anywhere
        function (reader) {                   // to turn pages.
            var stencil = new Monocle.Controls.Stencil(reader);  // Make internal links work.
            reader.addControl(stencil);
            var toc = Monocle.Controls.Contents(reader);         // Add a table of contents.
            reader.addControl(toc, 'popover', { hidden: true });
            createBookTitle(reader, { start: function () { reader.showControl(toc); } });
        }
    );
}

// This adds the book title to the top of each page.
function createBookTitle(reader, contactListeners) {
    var bt = {}
    bt.createControlElements = function () {
        cntr = document.createElement('div');
        cntr.className = "bookTitle";
        runner = document.createElement('div');
        runner.className = "runner";
        runner.innerHTML = reader.getBook().getMetaData('title');
        cntr.appendChild(runner);
        if (contactListeners) {
            Monocle.Events.listenForContact(cntr, contactListeners);
        }
        return cntr;
    }
    reader.addControl(bt, 'page');
    return bt;
}
</script>
<link rel="stylesheet" type="text/css" href="css/monocore.css" />
<link rel="stylesheet" type="text/css" href="css/monoctrl.css" />
<style type="text/css">
body {
    background: #eef;
    font-family: "sans-serif";
}
h1 {
    text-align: center;
}
#reader {
    width: 450px;
    height: 600px;
    border: 1px solid black;
    margin: 0 auto;
    background: white;
}
#reader p {
    margin: 1em;
}
.runner {
    font-variant: small-caps;
    font-size: 87%;
    color: #900;
}
.bookTitle {
    position: absolute;
    top: 0%;
    width: 100%;
    text-align: center;
    cursor: pointer;
}
body > p {
    width: 450px;
    margin: 1em auto;
}
</style>
</head>

<body>
<h1>EFM &mdash; Epub for Monocle</h1>
<div id="reader">
<p>Select an Epub file to read:
<input type="file" id="file" accept="application/epub+zip" onchange="fileSelected(event)" />
</p>
</div>

<p>This is a demonstration of an Epub reader based on <a href="http://monocle.inventivelabs.com.au/">Monocle</a>, implemented entirely in Javascript.  It uses the <a href="https://github.com/rschroll/efm">EFM library</a>, which should be able to deal with many Epub2 and Epub3 files.  If you're interested, you can see the <a href="https://github.com/rschroll/efm/tree/gh-pages">code for this example</a>.</p>
</body>
</html>
