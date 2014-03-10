EFM - Epub for Monocle
======================
Epub for Monocle is a pure Javascript implementation of [Monocle][1]'s
[book data interface][2] for Epub2 and Epub3 files.  This means that you
can use Monocle to load Epub files in a completely client-side manner.
[1]: http://monocle.inventivelabs.com.au/ "Monocle"
[2]: https://github.com/joseph/Monocle/wiki/Book-data-object "Monocle Wiki"

[See it][3] in action, and check out [this branch][4] to see how EFM is
deployed.
[3]: http://rschroll.github.com/efm "EFM Demonstration"
[4]: https://github.com/rschroll/efm/tree/gh-pages "gh-pages branch"

Usage
-----
EFM uses the [zip.js][5] library for unzipping the Epub files, so you'll
need that.  And of course, you need [Monocle][1] to actually display
the ebook in your browser.
[5]: http://gildas-lormeau.github.com/zip.js/ "zip.js library"

EFM provides a `Epub` object, which implements the book data interface.  It
takes two arguments for its constructor: the Epub file as an [HTML5 file
object][6] and a callback to be called when the `Epub` object has been
initialized.  The callback is necessary because the zip.js library works
asynchronously, so the parsing of the Epub file will not be done until
after the `Epub` object is constructed.
[6]: http://www.w3.org/TR/FileAPI/ "W3C File API"

Thus, if we have a file input with `id="file"` and a div with `id="reader"`
for the Monocle reader, the simplest code to render the Epub file selected
in the file input is
```javascript
var file = document.getElementById("file").files[0];
new Epub(file, function (bookData) {
    Monocle.Reader("reader", bookData);
});
```
With a modern browser on a modern machine, EFM is reasonably snappy.  I can
load _Moby Dick_ in under 1 second on my laptop, for example.

### Working with remote Epub files

EFM is designed to work with local files, since Monocle is designed for
working with remote files.  But instead of dealing with the remote Epub
file directly, Monocle trusts that you will convert it to a [book data
object][2] on the server.  This is much better than doing the conversion
on the client with EFM, since the server has known capabilities, the server
is generally more powerful than the clients, and this doesn't require the
client to download as much javascript.  If you're worried about the impact
on the server, you can always do the conversion offline and upload the
unzipped Epub file and the [book data object][2] to the server.  This means
that no conversion is needed whenever a client requests the book.  Think
of all the electrons you'll save!

That said, it is possible for EFM to work with remote Epub files.  The
first argument of the `Epub` object can be a [HTML5 blob object][7], rather
than a file object.  Conveniently, an [XMLHttpRequest][8] can be made to
return a blob.  Thus, the simplest code to display a remote Epub file is
```javascript
var request = new XMLHttpRequest();
request.open("GET", "url/of/file.epub", true);
request.responseType = "blob";
request.onload = function () {
    new Epub(request.response, function (bookData) {
        Monocle.Reader("reader", bookData);
    });
};
request.send();
```
But before you do this, please think long and hard if there isn't a better
way.  Think of the electrons!
[7]: http://www.w3.org/TR/FileAPI/#dfn-Blob "W3C File API"
[8]: https://developer.mozilla.org/en-US/docs/DOM/XMLHttpRequest/Sending_and_Receiving_Binary_Data "MDN Documentation"

Implementation Notes
--------------------
* I am a complete novice at Javascript, as my code demonstrates.  Please
  don't laugh too hard.  Better yet, send a pull request with fixes.

* At this point, EFM is more a proof-of-concept.  There is little error
  checking or reporting.  Valid Epub files should be handled correctly,
  but invalid ones will likely produce all sorts of unexpected and
  fascinating behavior.

* If you are serving the HTML file from `file://`, you will need to
  launch Chrome with the `--allow-file-access-from-files` flag. Firefox
  works fine by default.

* Some resources from some Epub files will not be loaded correctly.  For
  the sake of this explanation, let's divide the contents of an Epub
  archive into three classes: control files describe the contents of the
  Epub file, spine files are the HTML files that contain the text of the
  book, and auxiliary files are referenced by the spine files.  The
  control files are parsed by EFM into a form usable by Monocle, and the
  contents of the spine files are passed to Monocle as requested.  But
  Monocle (apparently) has no way to request the auxiliary files when
  they are referenced.  Thus, your web browser will attempt to fetch
  these files from the same place that served the HTML file, and will
  fail to find them.

  To attempt to mitigate this problem, EFM looks through spine files for
  images or stylesheet links that refer to auxiliary files.  The targets
  of these links are replaced by data URLs that encode the contents of
  the auxiliary files.  In many cases, this is enough.  However, it is
  possible for auxiliary files to reference other auxiliary files (a
  stylesheet referencing a font, for example, or an SVG illustration
  referencing a raster image).  This could be dealt with with a 
  multiple-pass system to sweep up all the auxiliary files, but such
  and approach has not been implemented.
  
  Such a system would be a rather large undertaking, as we would have
  to parse all types of files to find all possible references to other
  files in the Epub.  For most cases, the current system is good enough,
  so I won't be working on this mechanism.  But I do accept pull requests!

License
-------
EFM is distributed under the MIT license.
