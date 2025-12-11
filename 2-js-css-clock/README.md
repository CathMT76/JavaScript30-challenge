# 02 - JS + CSS Clock

![A green and white clock against a pale blue background with autumn leaf illustrations.](https://github.com/CathMT76/JavaScript30-challenge/blob/5d8f0fbaf591e20d649a5254c538de1dcf8da2be/2-js-css-clock/screenshot-day-2.jpg)

Demo: [JS and CSS Clock](https://cathmt76.github.io/JavaScript30-challenge/2-js-css-clock/)

## Key concepts

### 1. CSS `transform-origin` on clock "hands"

Since the default pivot point is `center`, `transform-origin: 100%` is used to mimic the pivot point of actual clock hands.

### 2. CSS `rotate()` to set correct zero point

The clock hands are `div` HTML elements which are block-level by default and thus, occupy the entire horizontal space of the container.

Because of this, the starting position of these "clock hands" are at the 9 o'clock position:

![Screenshot of a clock with all clock hands pointing in the 9 o'clock direction.](https://github.com/CathMT76/JavaScript30-challenge/blob/305cfaf7ed77abe57af733680244f6c4f661c0f3/2-js-css-clock/readme-1.jpg)

In order to mimic an actual clock hand's zero point 🕛, `transform: rotate(90deg)` is applied to set the starting point at 12 o'clock position:

![Screenshot of a clock with all clock hands pointing in the 12 o'clock direction.](https://github.com/CathMT76/JavaScript30-challenge/blob/305cfaf7ed77abe57af733680244f6c4f661c0f3/2-js-css-clock/readme-2.jpg)

### 3. Use of `cubic-bezier()` to add "snappiness" to the ticking motion

```CSS
transition-timing-function: cubic-bezier(0.1, 2.7, 0.58, 1)
```

The P1 ordinate is deliberately set outside the [0, 1] range to add a "snap-back" effect to the clock hands.
