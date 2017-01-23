# Basic PinPIE site

## Description
Meet some basic things, like pages, chunks, snippets, templates, placeholders.

***Goal***

Become familiar with some PinPIE tags.

***Code***

[Available at GitHub](https://github.com/pinpie/example-basic)

## Installation

```
git clone https://github.com/pinpie/example-basic
cd example-simplest
composer install
```

Or you can [download](https://github.com/pinpie/example-basic/archive/master.zip) it manually from the repo.

## Files
- /index.php — an entry point
- /pages/index.php — a page
- /pages/about.php — another page
- /css/css.css — some css
- /chunks/lorem/ipsum.php — some text chunk
- /snippets/rand.php — a snippet outputting a random number
- /templates/default.php — template with css in head and title with placeholder

### /index.php
The main entry point to include composer autoload or PinPIE standalone autoload and create PinPIE instance. It will detect requested page, check it exists and execute its code to serve requested content.

```PHP
include __DIR__ . '/vendor/autoload.php';
// include __DIR__ . '/pinpie/autoload.php';
\pinpie\pinpie\PinPIE::newInstance();
```

### /chunks/lorem/ipsum.php

A piece of text to be printed on the page. PHP code in chunks is not executed.

```HTML
<p>Lorem ipsum dolor sit amet...
```

### /snippets/rand.php
A piece of PHP code. It will be executed and result will be outputed to the page.

```PHP
echo rand(1, 999);
```

### /templates/default.php
A wrapper for page output

```HTML
<html>
<head>
  <!-- A static tag to link css file in the head -->
  [[%css=/css/css.css]]
  <!-- A title placeholder to get a title from the page file and put into the page head -->
  <title>[[*title]]</title>
</head>
<body>
<article>
  <header>
    <!-- Title placeholder to draw the title on the page -->
    <h1>[[*title]]</h1>
  </header>
  <!-- A content placeholder is a place, where PinPIE will output the page file content -->
  [[*content]]
</article>
</body>
</html>
```
### /pages/index.php

URL: /
Main page. Available at the / URL.
It contains PinPIE tags: constant, snippet, static tag and chunk.

```HTML
<!-- A title text. It goes to placeholder in the template -->
[title[=Hello]]

<p>Hi!</p>

<!-- A snippet of PHP code, it outputs some random number each time page is rendered. -->
<p>The answer is [[$rand]].</p>

<!-- A static tag. It will be rendered as <img... with width and height (optional), see below -->
[[%img=/images/cat.jpg]]

<p>Now visit <a href="/about">another page</a>.</p>

<!-- A chunk tag. Piece of plain text which can be used anywhere. -->
[[lorem/ipsum]]
```

After page is processed, its HTML code will look like that:
```HTML
...
<!-- Article and header are located in the template.
 Title was set in the template with a placeholder.
 You can find template code below. -->
<article>
  <header>
    <h1>Hello</h1>
  </header>
  
<!-- A title text. It is now above this line. -->

<p>Hi!</p>

<!-- A snippet of PHP code generated a number. -->
<p>The answer is 453.</p>

<!-- A static tag become an image with a hash preventing caching changed files.
  That hash will remain the same until file is changed. -->
<img src="//test.ru/images/cat-1.jpg?time=d9c8899d5833a0616ad2aef0bc2229cd" width="640" height="427">

<p>Now visit <a href="/about">another page</a>.</p>

<!-- A chunk tag. Piece of plain text which can be used anywhere. -->
<p>Lorem ipsum dolor sit amet...
```

### /pages/about.php
URL: /about
Another simple page to see how PinPIE handles URLs like /about

### /css/css.css
Just some styles to make sure file was loaded and affected the page view.



## What is PinPIE?
PinPIE is lightweight php-based engine for small sites

Read more about PinPIE engine in [PinPIE repo](https://github.com/pinpie/pinpie).