### gboad maddy

You see this everyday if you use android.

?<³|⁰([{⁰|%f¹&<=f{³&f"{%)

Author: Finch  
Points: 500

---

At first, it looks like random symbols, which might hint to some encoding. But the title and description point to Android's default keyboard, the Google Gboard. This leads us to the fact that when pressing and holding down certain keys on Android, it presents us with a symbol.

<img src="https://github.com/jiitinfosec/ctf-writeups-2020/blob/master/zh3r0%20CTF/crypto/gboad%20maddy/image.jpeg?raw=true" alt="gboard" width="400"/>


One can see the accented symbols, and reverse it to their original keys. Certain symbols like `⁰` are not visible via accents, but they do show up when pressing respective keys.  
`0 -> ⁰`  
`3 -> ³`  
`( -> {`

Notice how there is `f` used multiple times, since it was the only non-symbol, and holding `f` gave us `_`, we used it the other way around.

This gives us the following string,
`mu3e0{to0eq_1gur_o3g_xoq}`

Applying ROT13, we get
`zh3r0{gb0rd_1the_b3t_kbd}` (25 characters)

While it looks like the final flag, it isn't. (notice how the flag string doesn't really make sense)

We were given a hint, len(flag) = 28
We knew we had to add 3 charaters, and the obvious candidate was to make it read, `gb0rd_is_the_best_kbd`.

#### Flag
`zh3r0{gb0rd_1s_the_b3st_kbd}`


