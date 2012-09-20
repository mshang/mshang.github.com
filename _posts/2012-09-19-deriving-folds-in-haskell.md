--- 
status: publish
title: Deriving Folds in Haskell
meta: 
  _edit_last: "1"
layout: post
tags: []

published: true
type: post
---

[Folds](http://en.wikipedia.org/wiki/Fold_(higher-order_function)) are fundamental operations in functional programming. There are two basic types of linear folds: left folds and right folds. Superficially, they sound like symmetric versions of one another. In reality, the difference between them is important but subtle.

# Right fold

Consider a list: `[1,2,3]`. In Haskell, this is syntactic sugar for `1:(2:(3:[]))`. Right folds are simple: they replace all occurrences of the cons operator `:` with some operator `` `f` ``, and the empty list `[]` with some initial value `z`.

Let the symbol `~~` mean "is equivalent to".

    foldr f z [1,2,3] ~~ 1 `f` (2 `f` (3 `f` z))

*Example: (sum of a list)*

    foldr (+) 0 [1,2,3] ~~ 1 + (2 + (3 + 0)) ~~ 6

*Example: (identity)*

    foldr (:) [] [1,2,3] ~~ 1 : (2 : (3 : [])) ~~ [1,2,3]

Implementing `foldr` recursively is straightforward. As usual, we trust the function to do the right thing for a reduced part of the input. In this case, we trust that `foldr` makes the appropriate substitutions for just the tail of the input list. If we are trying to get from `1:(2:(3:[]))` to ``1 `f` (2 `f` (3 `f` z))``, we trust that `foldr f z (2:(3:[]))` indeed gives ``2 `f` (3 `f` z))``. Then we can have ``foldr f z (1:(2:(3:[]))) = 1 `f` (foldr f z (2:(3:[])))``. In general, we define the induction step as:

    foldr f z (x:xs) = x `f` (foldr f z xs)

Note that in each recursive call of `foldr`, the second parameter is not altered. This is not the case for left folds.

Now consider the base case. By successively taking the tail of a list, we will eventually reach the empty list. In that case, by definition, the result should be `z`:

    foldr _ z [] = z

Due to the nature of pattern matching in Haskell, the base case definition should be placed above the induction step definition.

# Left fold

Left folds are more difficult to understand. Intuitively, if `foldr` produces ``1 `f` (2 `f` (3 `f` z))``, then `foldl` produces ``((1 `f` 2) `f` 3) `f` z``. If `` `f` `` is associative, then these are equivalent. In particular, `+` is associative, but `:` is not. To express left fold in Haskell, it is easiest to start with a specific case and then generalize. One of the canonical examples of a left fold is `reverse`, which reverses a given list. It would be reasonable to guess that we could define `reverse` recursively, using the form:

    reverse []     = []
	reverse (x:xs) = ___ reverse ___

However, if you stare at this for long enough, you will see that it is a dead end. When we assume that the subcall to `reverse` returns the correct result for some reduced part of the input, the only reasonable candidate is the tail `xs`. This does not help, as we cannot easily append to a list. Instead, we need an accumulator: another parameter on which to recurse in order to keep track of the intermediate result.

    reverse = aux [] where
      aux acc [] = acc
      aux acc (x:xs) = aux (x:acc) xs

We start with an empty accumulator. At each inductive step, we advance along the input list and cons an element to the accumulator. Eventually, we reach the end of the input, at which point the accumulator holds exactly the result that we want and we return it all the way up the chain.

To get `foldl`, we generalize away from the cons operator in `(x:acc)`, replacing it with a more general `` `f` ``.

    foldl _ acc []     = acc
	foldl f acc (x:xs) = foldl (acc `f` x) xs

Note the order of the operands of `` `f` ``. This is to obtain the same linear order as `foldr`. In particular:

    reverse = foldl (flip (:)) []

`reverse` corresponds naturally to `foldl`, as the identity function on lists corresponds naturally to `foldr`. From this, we can intuit the fact that `foldr` works on infinite lists whereas `foldl` does not. After all, what would be the meaning of `reverse [1..]`? Interestingly, `head $ reverse $ reverse [1..]` does not work. Why? Left as an exercise for the reader.
