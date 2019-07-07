--- 
status: publish
title: Odds and Powers of Two
meta: 
  _edit_last: "1"
layout: post
tags: []

published: false
type: post
---
Every positive integer can be uniquely expressed as an odd number times a power of two. In case this factoid isn't immediately obvious to anyone, as it wasn't to me, here's why:

By the Fundamental Theorem of Arithmetic, any positive integer has a unique prime factorization. Since the only even prime is two, this factorization will consist of zero or more twos, and the rest will be odd primes. An odd times an odd gives odd. If you multiply together all the twos, you get your power of two. If you multiply together all the others, you get your odd number. The uniqueness of this factorization follows from the uniqueness of the prime factorization.
