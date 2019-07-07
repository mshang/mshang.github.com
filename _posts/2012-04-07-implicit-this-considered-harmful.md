--- 
status: publish
title: Implicit "this" Considered Harmful
meta: 
  _edit_last: "1"
layout: post
tags: []

published: false
type: post
---

Finally, my own entry into the venerable "X Considered Harmful" series of articles. Today, I would like to discuss what I've learned about code readability from dabbling around in Javascript. Code readability... I have searched far and wide for that elusive goal. From Python, I learned to detest curly braces and semicolons. From CoffeeScript, I learned to love the fat arrow. From C, I learned to appreciate being able to tell a reference from a variable. But what is there to learn from Javascript, the ugliest of the ugly? Personally, I have learned that scope is very important for code readability. Nobody is claiming that Javascript has sane scoping; function scope is awful. However, because Javascript doesn't have classes, it was forced to do one thing right: the `this` keyword. Every time you call a member function or use a member variable, you must preface it with `this.`. In C++, this is optional, i.e. implicit `this`. As a result, when you're reading over a method, it's not immediately obvious where each variable comes from. There are three possibilities:

* The variable is a member variable.
* The variable was passed in as an argument.
* The variable was declared inside the method.

In order to disambiguate the first option, some programmers prefix all member variables with `m_`. I dislike this notation because it might confuse people reading your code who are unfamiliar with the practice. Instead, it's best for the notation to have some meaning defined in the language itself, even if it is redundant. That's why it's good practice to preface all member variables with `this->`. To some, this might reek of Java-esque verbosity (although Java also has implicit `this`). I would counter with [this article](http://www.informit.com/articles/article.aspx?p=1824790), and specifically a quote from Josh Bloch:

> A little redundancy in a language is a good thing. It's important for readability.

Not all redundancy is helpful; you have to pick the right constructs. For example, curly braces and semicolons just get in the way. While I don't expect Java or C++ to change, as long as we're stuck with them, we should do what we can to make our code readable.
