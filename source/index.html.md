---
title: Retype documentation

language_tabs:
  - javascript
  - html

toc_footers:
  - <a href='https://github.com/kgiszczak/retype'>Source Code</a>
  - <a href='https://github.com/tripit/slate'>Powered by Slate</a>

search: true
---

# Introduction

Library to save and restore cursor position on contenteditable elements. You can use it to create functionality like Twitter's hashtags. It works by inserting special character in place of cursor, manipulating the text and then replacing this special character with cursor.

You can find source code [here](https://github.com/kgiszczak/retype).

# Installation

jQuery is required for this plugin to work. In your HTML file, load simply by: `<script src="retype.min.js"></script>`
Both the minified and uncompressed (for development) versions are in the `/dist` directory.

# Usage

This plugin works on contenteditable elements.

## Simple usage

```html
<div id="editor" contenteditable="true" spellcheck="false"></div>
```

```javascript
$('#editor').retype('#!');
```

Initialize it with string containing triggering characters. Everytime you type one of those characters it will be replaced with html tag.

<div class="editor-wrapper">
  <div id="editor1" class="editor" contenteditable="true" spellcheck="false">Lorem ipsum #dolor sit !amet.</div>
</div>

<script>
  $('#editor1').retype('#!');
</script>

## Full control

```html
<div id="editor" contenteditable="true" spellcheck="false"></div>
```

```javascript
$('#editor').retype(function() {
  var html = $(this).html();
  var c = $.retype.CARET_CHAR;

  html = html.replace(/<\/?span[^>]*>/ig, '');

  html = html.replace(new RegExp('f' + c + '?o' + c + '?o', 'ig'),
    '<span class="tag tag1">$&</span>');
  html = html.replace(new RegExp('b' + c + '?a' + c + '?r', 'ig'),
    '<span class="tag tag2">$&</span>');
  html = html.replace(new RegExp('b' + c + '?a' + c + '?z', 'ig'),
    '<span class="tag tag3">$&</span>');

  $(this).html(html);
});
```

If you want to have full control over what is replaced you can initialize this plugin with callback function. For example to wrap every occurance of words `foo`, `bar` or `baz` with a span element you can do it like this:

<div class="editor-wrapper">
  <div id="editor2" class="editor" contenteditable="true" spellcheck="false">Lorem foo ipsum bar dolor baz sit amet</div>
</div>

<script>
  $('#editor2').retype(function() {
    var html = $(this).html();
    var c = $.retype.CARET_CHAR;

    html = html.replace(/<\/?span[^>]*>/ig, '');

    html = html.replace(new RegExp('f' + c + '?o' + c + '?o', 'ig'), '<span class="tag tag1">$&</span>');
    html = html.replace(new RegExp('b' + c + '?a' + c + '?r', 'ig'), '<span class="tag tag2">$&</span>');
    html = html.replace(new RegExp('b' + c + '?a' + c + '?z', 'ig'), '<span class="tag tag3">$&</span>');

    $(this).html(html);
  });
</script>
