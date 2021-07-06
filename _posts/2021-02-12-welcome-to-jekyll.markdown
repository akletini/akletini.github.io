---
layout: post
title: "Bachelor Thesis on text comparison algorithms"
date: 2021-07-06 12:00:40 +0100
categories: jekyll update
---

This article will explain some special aspects of the software MultiTextCompare, which was developed during my bachelor thesis. Its main goal is to be able to compare any amount of text-based files (txt, xml, json), calculate a similarity rating for them and be able to show their diff for up to 3 files. Everything is done in Java 7... (let's not talk about that one).

![image](/assets/images/Matrix_final.png)

The easiest approach is to compare two files at a time, while checking for equality of the given strings within the current line. Since equality is merely an extreme case of similarity, this approach is not sufficient.

There needs to be a way to measure the similarity of two given strings and there is:

The concept of an edit distance can quantify how dissimilar two strings are by counting how many steps it would take to convert one string into another. With some additional math, this dissimilarity can be turned into a similarity percentage. While this solves the problem for a missing similarity rating, it still doesnt tell you how similar two files really are. What if they are indeed equal but one file has a line break at the start and every equal line is misaligned?

Some additional thinking is needed for this. Maybe one could match similar strings within different lines and align them to be written on the same line index. More math... yay!

While this might work for regular text files, XML- and JSON-files underlie a certain structure and contain a lot of markup, which adds additional overhead for calculations and may influence result quality. Especially on short lines, there may be a high impact of markup characters compared to actual content. Thankfully there are some powerful libraries in JDOM and Jackson to parse those two formats and compare their contents via the document trees. The principle here is to basically match equally named nodes of the corresponding tree graphs and compare their contents. This approach cuts out all possible markup and makes sure to only compare contexually similar nodes. Again this is more math and additionally some recursive programming thus being a lot of ~~pain~~ fun.

The codebase will be supplied on GitHub as soon as the project is finished :)
