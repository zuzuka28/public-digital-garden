---
{"dg-publish":true,"permalink":"/notes/organize.resource.it.obsidian-web-clipper-bookscript/","title":"Obsidian Web Clipper Bookscript"}
---


[[organize.resource.pkm.app.bookmarklet-maker \| Добавить этот скрипт как закладку в браузере]]

<https://gist.github.com/kepano/90c05f162c37cf730abb8ff027987ca3>

```javascript
Promise.all([
  import("https://unpkg.com/turndown@6.0.0?module"),
  import("https://unpkg.com/@tehshrike/readability@0.2.0"),
]).then(async ([{ default: Turndown }, { default: Readability }]) => {
  /* Optional vault name */
  const vault = "";

  /* Optional folder name such as "Clippings/" */
  const folder = "clipbox/";

  /* Optional tags  */
  let tags = "source.clip";

  /* Parse the site's meta keywords content into tags, if present */
  if (document.querySelector('meta[name="keywords" i]')) {
    var keywords = document
      .querySelector('meta[name="keywords" i]')
      .getAttribute("content")
      .split(",");

    keywords.forEach(function (keyword) {
      let tag = " " + keyword.split(" ").join("");
      tags += tag;
    });
  }

  function getSelectionHtml() {
    var html = "";
    if (typeof window.getSelection != "undefined") {
      var sel = window.getSelection();
      if (sel.rangeCount) {
        var container = document.createElement("div");
        for (var i = 0, len = sel.rangeCount; i < len; ++i) {
          container.appendChild(sel.getRangeAt(i).cloneContents());
        }
        html = container.innerHTML;
      }
    } else if (typeof document.selection != "undefined") {
      if (document.selection.type == "Text") {
        html = document.selection.createRange().htmlText;
      }
    }
    return html;
  }

  const selection = getSelectionHtml();

  const { title, byline, content } = new Readability(
    document.cloneNode(true),
  ).parse();

  function getFileName(fileName) {
    var userAgent = window.navigator.userAgent,
      platform = window.navigator.platform,
      windowsPlatforms = ["Win32", "Win64", "Windows", "WinCE"];

    if (windowsPlatforms.indexOf(platform) !== -1) {
      fileName = fileName.replace(":", "").replace(/[/\\?%*|"<>]/g, "-");
    } else {
      fileName = fileName
        .replace(":", "")
        .replace(/\//g, "-")
        .replace(/\\/g, "-");
    }
    return fileName;
  }
  const fileName = getFileName(title);

  if (selection) {
    var markdownify = selection;
  } else {
    var markdownify = content;
  }

  if (vault) {
    var vaultName = "&vault=" + encodeURIComponent(`${vault}`);
  } else {
    var vaultName = "";
  }

  const markdownBody = new Turndown({
    headingStyle: "atx",
    hr: "---",
    bulletListMarker: "-",
    codeBlockStyle: "fenced",
    emDelimiter: "*",
  }).turndown(markdownify);

  /* YAML front matter as tags render cleaner with special chars  */
  const fileContent =
    "---\n" +
    'title: "' +
    title +
    '"\n' +
    "source: " +
    document.URL +
    "\n" +
    "topics: \n" +
    "tags: [" +
    tags +
    "]\n" +
    "---\n\n" +
    markdownBody;

  document.location.href =
    "obsidian://new?" +
    "file=" +
    encodeURIComponent(folder + fileName) +
    "&content=" +
    encodeURIComponent(fileContent) +
    vaultName;
});
```
