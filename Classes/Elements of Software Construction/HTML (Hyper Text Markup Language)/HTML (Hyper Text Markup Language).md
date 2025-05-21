---
aliases:
  - HTML
---

a language that defines content and structure of a web document

Each *element* is defined by an **OPEN** and **CLOSE** tag

Follows the following format:
- html
- head
    - meta
    - title
    - text
- body
    - paragraph
    - text

## `<head>`
contains metadata (data about data)

examples of metadata:
- `<title>`: title of the document **(required)**
- `<link>`:  used to link to external style sheets **([[CSS (Cascading Style Sheets)]] file)**
- `<meta>`: to  specify
	- character set
	- page description
	- keywords
	- author of the document
	- viewport settings
- `<script>`: define client-side JavaScripts (referenced as .js or written JS code)

![[HTML-1.webp]]

## `<body>`
contains *headings, paragraphs, images, hyperlinks, tables, lists, etc.*

Examples:
```html
<a href="https://sutd50003.github.io/">Visit 50.003 homepage</a>
```
The **href attribute** of `<a>` specifies the **URL of the page** the link goes to

```html
<img src=”Elephant.jpg" width="500" height="600">
```
The **src attribute** of `<img>` specifies the **path to the image** to be displayed. The *width* and *height* specify the *image size*