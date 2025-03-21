# Bug: web animation cancel() followed by animate() behave oddly when requestAnimationFrame's involved

> Issue #31634 - Created on 11/26/2024

> Original URL: https://github.com/facebook/react/issues/31634

## Description

See repro: [tinyurl.com/4u85ehnh](https://t.co/3eMtHJfEQ5)

Video of the glitch: https://x.com/_chenglou/status/1860978002643063054

Tldr on button click I cancel the existing animation and in `useLayoutEffect` I start a new one. The animation goes from translate 100px to 200px. However, clicking on the button will show a split second glitched unstyled view of the animated text (position at 0px) before jumping to 100px and animating to 200px. Commenting out the `requestAnimationFrame` wrapper inside `handleClick` solves it.

Happens across Chrome, Safari and Firefox.

Notes:
- The rAF happens on the same frame as everything else, so there shouldn't be any visible DOM repaint
- Even if the rAF is executed later, it'd means `cancel()` is executed _later_, which should hide the unstyled visual, not reveal it
- Although, the fact is that rAF can be _scheduled_ earlier, if this is relevant: https://x.com/nomsternom/status/1853687984266055983 (original post unrelated to this issue)
- You can check the difference in console.logs. The microtask log result & order is different. The logs themselves (including getComputedStyle which forces reflows) don't disturb this repro
- FWIW, I was wondering whether the first frame of `animate()` is skipped when `cancel()` is done in the rAF, and it seems it's preserved. Another debugging video (first 6 times glitching, 7th time not) below. The first frame's position is 100px, which is where the red square is. For alignment. Here:

https://github.com/user-attachments/assets/c7a9a21f-57e7-4123-bac5-8a07a02741f4

I'd also like to be able to get a clean, React-less repro but not sure how complicated that'd be.
