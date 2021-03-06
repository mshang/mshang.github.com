--- 
status: publish
title: Anti-aliasing in HTML5 canvas
meta: 
  _edit_last: "1"
layout: post
tags: []

published: false
type: post
---
If you take a look at my recently improved [syntax tree generator](http://mshang.ca/syntree), you might notice that the appearance of the lines depends on what browser you're using. That's because anti-aliasing is an implementation-defined feature for HTML5 `<canvas>` ([source](http://stackoverflow.com/questions/4261090/html5-canvas-and-anti-aliasing)). When you tell the canvas to draw a line, how that line looks depends entirely on what browser you're using. This is a terrible oversight on the part of WHATWG, the group responsible for the HTML5 standard. It's nice to have your page to look similar across browsers. However, you **definitely** want your primitives, such as lines and circles to look identical across browsers. Otherwise, it defeats the purpose of having something as low level as `<canvas>`, which is to provide more fine-grained control of appearance than CSS does.
