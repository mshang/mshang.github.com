--- 
status: publish
title: TeX Tricks
meta: 
  _edit_last: "1"
layout: post
tags: []

published: true
type: post
---
One day, I hope to learn some real TeX, but until that day comes, I search and ask questions on [tex.stackexchange.com](http://tex.stackexchange.com/). Recently, I wanted to define a command that would behave differently depending on whether or not it was invoked in a math environment. From [this](http://tex.stackexchange.com/questions/15193/opposite-of-ensuremath-ensure-that-im-not-in-math-mode) thread, I found out about the command [`\ifmmode`](http://en.wikibooks.org/wiki/TeX/ifmmode). For example, if you wanted a command `\mbb` to produce blackboard type in text and in math:

    \newcommand{\mbb}[1]{\ifmmode \mathbb{#1}\else $\mathbb{#1}$\fi}

I'm sure it's better to do it in TeX with `\def`, but I know much about that. Note that `\mathbb` throws an error when it's used outside of a math environment, but `\mbb` works fine in both math and text.

Another thing that I wanted was code folding. As far as I know, Texworks folds only "`\part`, `\chapter`, `\section`,..., `\begin{foo}` `\end{foo}` blocks" (from the User Manual). I wanted to create a non-functional custom environment so that I could fold arbitrary parts, like all the `\usepackage` statements. In Visual Studio, I would do this using `#pragma region`. Unfortunately, this didn't work (threw an error) so I [asked for help](http://tex.stackexchange.com/questions/44022/code-folding-in-latex). Using the hint that I got, I made a workaround, which is just to comment out a `\begin{foo}` statement. It still folds. However, I still would like to learn enough TeX to implement my original solution. From the little that I saw, it seems like a powerful and dangerous language.

**Edit:** I just realized that Texmaker actually folds the entire header. Oh well, I still think that little trick is useful.
