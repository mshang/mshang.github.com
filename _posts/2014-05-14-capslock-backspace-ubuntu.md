--- 
status: publish
title: Switching Caps Lock and Backspace in Ubuntu 14.04
meta: 
  _edit_last: "1"
layout: post
tags: []

published: true
type: post
---

I made a patch file that switches the Caps Lock and Backspace keys in Ubuntu 14.04 by changing some X config files.

    > wget mshang.ca/xkb_capslock_delete.patch
    # Make sure it looks safe.
    > less xkb_capslock_delete.patch
    > sudo patch -d/ -p0 < xkb_capslock_backspace.patch
