--- 
status: publish
title: Probabilistic Algorithms
meta: 
  _edit_last: "1"
layout: post
tags: []

published: true
type: post
---
My supervisor <a href="http://www.math.mcgill.ca/jcnave/" target="_blank">Prof. Nave</a> is always telling me that probabilistic algorithms can give surprisingly good results. Recently, I've discovered for myself how amazing they can be.

Here are two examples that provide vastly better solutions than deterministic algorithms:

<strong><a href="http://en.wikipedia.org/wiki/Bloom_filter" target="_blank">Bloom filters</a></strong> are a very fast way to test if an element is a member of a set. They are probabilistic in the sense that once in a while, they will give a false positive. This means that they will indicate that an element is in a set when it actually isn't. They will never give a false negative. Note that Bloom filters are very simple data structures compared to search trees or hash tables. They don't actually store any data; they only store a binary state. However, what you give up in storage capability and false positives, you gain many times over in speed and size. Besides, you can always overlay a Bloom filter over a more traditional data structure to get the best of both worlds.

A post on reddit.com/r/programming led me to <a href="http://stackoverflow.com/questions/7153659/find-an-integer-not-among-four-billion-given-ones">this</a> stackoverflow question, which asks how to produce an integer that is not among a set of four billion given integers. I had actually already seen this problem in Jon Bentley's book <a href="http://www.amazon.com/Programming-Pearls-2nd-Jon-Bentley/dp/0201657880">Programming Pearls</a> (a great book, highly recommended). Bloom filters would not be appropriate here because how would we deal with false positives? The answer that caught my eye was <a href="http://stackoverflow.com/questions/7153659/find-an-integer-not-among-four-billion-given-ones/7156485#7156485">this one</a>. Essentially, the reply recommends randomly generating 1000 integers and testing them against the set. In the end, there is an overwhelmingly high chance that at least one of them will survive. Given memory limitations, this is certainly an excellent algorithm. Perhaps not elegant and exact like binary search, but small and fast.
