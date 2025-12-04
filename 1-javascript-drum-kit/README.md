# 01 - JavaScript Drum Kit

![Screenshot of HTML drum kit. There are nine buttons labelled with the corresponding drum sound.](https://github.com/CathMT76/JavaScript30-challenge/blob/e3abce7bcf02fee193dee39701699813ce7587fc/01%20-%20JavaScript%20Drum%20Kit/screenshot-day-1.png)

Demo: [JavaScript Drum Kit](https://cathmt76.github.io/JavaScript30-challenge/1-javascript-drum-kit/)

## Key concepts

### 1. `addEventListener()` for `keydown` event

```
window.addEventListener("keydown", playSound)
```

The script to play the corresponding drum sound (e.g. "snare") will fire on `keydown` of one of the "drum keys" (e.g. <kbd>J<kbd>).

### 2. Use of `data-*` for custom attributes

The drum key div and its corresponding sound are mapped using the `data-key` attribute. `data-key` in this case represents the `keyCode`of the pressed key.

The drum key `<div>`:

```
<div data-key="74" class="key">
        <kbd>J</kbd>
        <span class="sound">snare</span>
      </div>
```

The drum sound `<audio>`:

```
<audio data-key="74" src="sounds/snare.wav"></audio>
```

### 3. Obtain `keyCode` info from the event

When the `keydown` event is triggered, we use `e.keyCode` to identify which key has been pressed and to play the corresponding drum sound.

```
function playSound(e) {
        const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
        const key = document.querySelector(`.key[data-key="${e.keyCode}"]`);

        if (!audio) return;
        audio.currentTime = 0;
        audio.play();
      }
```

In the above, template literals are used to avoid the `=` in the attribute selector being mistaken for a variable assignment in JavaScript.

### 4. "Switch on" a CSS style on keydown: Use of `classList.add`

In this example, the drum key div should take on this CSS style on keydown:

**CSS**:

```
.playing {
  transform: scale(1.1);
  border-color: #ffc600;
  box-shadow: 0 0 1rem #ffc600;
}
```

So we use `classList.add` to add the class of `playing` to the drum key div that was pressed.

**JS**:

```
function playSound(e) {
        const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
        const key = document.querySelector(`.key[data-key="${e.keyCode}"]`);

        if (!audio) return;
        audio.currentTime = 0;
        audio.play();
        key.classList.add("playing");
      }
```

### 5. "Switch" CSS style back off: `addEventListener()` for `transitionend`

```
const keys = document.querySelectorAll(".key");
      keys.forEach((key) =>
        key.addEventListener("transitionend", removeTransition)
      );

```

We have to use a `forEach()` or loop to add the event listener at the individual div level as `transitionend` does not bubble up to the `Document` or `Window` level.

```
function removeTransition(e) {
        if (e.propertyName !== "transform") return;
        this.classList.remove("playing");
      }

```

Then `this.classList.remove("playing")` is used to remove the `playing` class from the div so it reverts to its default style.
