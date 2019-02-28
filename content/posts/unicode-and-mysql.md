---
title: "Which emojis can be stored in MySQL with utf8 encoding?"
tags: ["unicode", "mysql", "emojis", "utf8"]
date: 2019-02-22T14:28:57+01:00
draft: false
---

There are so many great articles on the web about Unicode and UTF-8 encoding already. For example:

- [David C.Zentgraf - What Every Programmer Absolutely, Positively Needs To Know About Encodings And Character Sets To Work With Text](http://kunststube.net/encoding/#fn:valid-utf8)

- [Joel Spolsky - The Absolute Minimum Every Software Developer Absolutely, Positively Must Know About Unicode and Character Sets (No Excuses!)](https://www.joelonsoftware.com/2003/10/08/the-absolute-minimum-every-software-developer-absolutely-positively-must-know-about-unicode-and-character-sets-no-excuses/)

**Unicode** provides a unique number for every character, no matter what the platform, no matter what the program, no matter what the language.
From: [What is Unicode?](http://unicode.org/standard/WhatIsUnicode.html)

**Unicode code point** is a way of written the unique number assigned for every character. It preceeded by a "U+" and the number is in hexadecimal. For example, letter _A_ is assigned to number _65_, and its code point is _U+0041_ `(65 = 0*4096 + 0*256 + 4*16 + 1)`

**UTF-8** is one way of encoding Unicode. We can think about it as representing Unicode code points in a way that computer can understand. There are other encodings as well, eg. UTF-16. UTF-8 and UTF-16 are _variable-length encoding_. It means that small number code point will be represented with less byte than large number code point.

Example:

| Letter | Code point | UTF-8 encoding      | Number of bytes |
|--------|------------|---------------------|-----------------|
| A      | U+0041     | 0x41                | 1               |
| Â      | U+00C2     | 0xC3 0x82           | 2               |
| ☂      | U+2602     | 0xE2 0x98 0x82      | 2               |
| ￦     | U+FFE6     | 0xEF 0xBF 0xA6      | 3               |
| 😇     | U+1F607    | 0xF0 0x9F 0x98 0x87 | 4               |

> MySQL’s “utf8” isn’t UTF-8.

> The “utf8” encoding only supports three bytes per character. The real UTF-8 encoding — which everybody uses, including you — needs up to four bytes per character.

From: [In MySql never use utf8, use utf8mb4](https://medium.com/@adamhooper/in-mysql-never-use-utf8-use-utf8mb4-11761243e434)




