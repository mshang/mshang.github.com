--- 
status: publish
title: Switching Caps Lock and Delete in OS X Mountain Lion
meta: 
  _edit_last: "1"
layout: post
tags: []

published: true
type: post
---

Although I don't use the Colemak keyboard layout, I like that it switches the Caps Lock and Delete (Backspace) keys. Switching them on my PC was easy using [AutoHotKey](http://www.autohotkey.com). Switching them in OS X Mountain Lion is a bit more challenging. There's an app called [PCKeyboardHack](http://pqrs.org/macosx/keyremap4macbook/pckeyboardhack.html.en) that does this. However, if you just switch the keycode mappings for Caps Lock and Delete in PCKeyboardHack, you run into the problem that if you press and hold the Caps Lock key, it will delete one and only one character. In other words, key repeat doesn't work properly. The cause of this problem is that OS X  disables key repeat for Caps Lock. The suggested fix on the PCKeyboardHack [usage](http://pqrs.org/macosx/keyremap4macbook/pckeyboardhack-usage.html.en) page is to disable Caps Lock in "System Preferences > Keyboard > Modifier Keys". If you do this, key repeat will indeed work properly, but now your Delete key won't work as Caps Lock. To get around this, you have to do a triple remap:

1.  In "System Preferences > Keyboard > Modifier Keys", remap Caps Lock to Control and vice versa.

    ![Modifier Keys settings](/images/modkeysettings.png)

2.  In PCKeyboardHack, remap:
    * CapsLock to Delete (keycode 51)
    * Delete to Control_L (keycode 59)
    * Control_L to CapsLock (keycode 57)
    
    ![PCKeyboardHack settings 1](/images/pckeyboardhack1.png)
    
    ![PCKeyboardHack settings 2](/images/pckeyboardhack2.png)

Now everything should work as expected.
