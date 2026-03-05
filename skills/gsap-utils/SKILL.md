---
name: gsap-utils
description: Use gsap.utils for clamping, distribution, interpolation, mapping, random, snapping, arrays, and strings. Use when the user asks about gsap.utils, clamp, mapRange, random, snap, toArray, wrap, or helper utilities in GSAP.
license: MIT
---

# gsap.utils

## When to Use This Skill

Apply when writing or reviewing code that uses **gsap.utils** for math, array/collection handling, unit parsing, or value mapping in animations (e.g. mapping scroll to a value, randomizing, snapping to a grid, or normalizing inputs).

## Overview

**gsap.utils** provides pure helpers; no need to register. Use in tween vars (e.g. function-based values), in ScrollTrigger or Observer callbacks, or in any JS that drives GSAP. All are on **gsap.utils** (e.g. `gsap.utils.clamp()`).

## Clamping and Ranges

### clamp(min, max, value)

Constrains a value between min and max.

```javascript
gsap.utils.clamp(0, 100, 150); // 100
gsap.utils.clamp(0, 100, -10); // 0
```

### mapRange(inMin, inMax, outMin, outMax, value)

Maps a value from one range to another. Use when converting scroll position, progress (0–1), or input range to an animation range.

```javascript
gsap.utils.mapRange(0, 100, 0, 500, 50);  // 250
gsap.utils.mapRange(0, 1, 0, 360, 0.5);    // 180 (progress to degrees)
```

### normalize(min, max, value)

Returns a value normalized to 0–1 for the given range. Inverse of mapping when the target range is 0–1.

```javascript
gsap.utils.normalize(0, 100, 50);  // 0.5
gsap.utils.normalize(100, 300, 200); // 0.5
```

### interpolate(start, end, progress)

Interpolates between two values at a given progress (0–1). Handles numbers, colors, and objects with matching keys.

```javascript
gsap.utils.interpolate(0, 100, 0.5);       // 50
gsap.utils.interpolate("#ff0000", "#0000ff", 0.5); // mid color
gsap.utils.interpolate({ x: 0, y: 0 }, { x: 100, y: 50 }, 0.5); // { x: 50, y: 25 }
```

## Random and Snap

### random(min, max, increment?)

Returns a random number between min and max. Optional **increment** snaps to steps (e.g. `increment: 1` for integers).

```javascript
gsap.utils.random(10, 20);           // e.g. 14.3
gsap.utils.random(1, 10, 1);         // integer 1–10
gsap.utils.random(-100, 100, 10);    // -100, -90, ..., 100
```

### snap(snapTo, value)

Snaps a value to the nearest multiple of **snapTo**, or to the nearest value in an array of allowed values.

```javascript
gsap.utils.snap(10, 23);     // 20
gsap.utils.snap(0.25, 0.7);  // 0.75
gsap.utils.snap([0, 100, 200], 150); // 100 or 200 (nearest in array)
```

Use in tweens for grid or step-based animation:

```javascript
gsap.to(".x", { x: 200, snap: { x: 20 } });
```

### shuffle(array)

Returns a new array with the same elements in random order. Use for randomizing order (e.g. stagger from "random" with a copy).

```javascript
gsap.utils.shuffle([1, 2, 3, 4]); // e.g. [3, 1, 4, 2]
```

### distribute(baseObject)

Distributes values across a range (e.g. for positioning many elements). Returns a function that, given an index and total, returns a value in the range. See GSAP docs for **base**, **amount**, **from**, **grid**, etc.

```javascript
const dist = gsap.utils.distribute({ base: 0, amount: 100, from: "center" });
dist(0, 5); // value for index 0 of 5
dist(2, 5); // value for index 2 of 5
```

## Units and Parsing

### getUnit(value)

Returns the unit string of a value (e.g. `"px"`, `"%"`, `"deg"`). Use when normalizing or converting values.

```javascript
gsap.utils.getUnit("100px");   // "px"
gsap.utils.getUnit("50%");     // "%"
gsap.utils.getUnit(42);        // "" (unitless)
```

### unitize(value, unit)

Appends a unit to a number, or returns the value as-is if it already has a unit. Use when building CSS values or tween end values.

```javascript
gsap.utils.unitize(100, "px");  // "100px"
gsap.utils.unitize("2rem", "px"); // "2rem" (unchanged)
```

### splitColor(color)

Splits a color string into RGB components (0–255) or an array. Use when animating color components or building gradients.

```javascript
gsap.utils.splitColor("#ff0000"); // [255, 0, 0] or similar
```

## Arrays and Collections

### selector(scope)

Returns a scoped selector function that finds elements only within the given element (or ref). Use in components so selectors like `".box"` match only descendants of that component, not the whole document. Accepts a DOM element or a ref (e.g. React ref; handles `.current`).

```javascript
const q = gsap.utils.selector(containerRef);
q(".box");        // array of .box elements inside container
gsap.to(q(".circle"), { x: 100 });
```

### toArray(value, scope?)

Converts a value to an array: selector string (scoped to element), NodeList, HTMLCollection, single element, or array. Use when passing mixed inputs to GSAP (e.g. targets) and a true array is needed.

```javascript
gsap.utils.toArray(".item");           // array of elements
gsap.utils.toArray(".item", container); // scoped to container
gsap.utils.toArray(nodeList);          // [ ... ] from NodeList
```

### pipe(...functions)

Composes functions: **pipe(f1, f2, f3)(value)** returns f3(f2(f1(value))). Use when applying a chain of transforms (e.g. normalize → mapRange → snap) in a tween or callback.

```javascript
const fn = gsap.utils.pipe(
  (v) => gsap.utils.normalize(0, 100, v),
  (v) => gsap.utils.snap(0.1, v)
);
fn(50); // normalized then snapped
```

### wrap(min, max, value)

Wraps a value into the range min–max (inclusive min, exclusive max). Use for infinite scroll or cyclic values.

```javascript
gsap.utils.wrap(0, 360, 370);  // 10
gsap.utils.wrap(0, 360, -10);  // 350
```

### wrapYoyo(min, max, value)

Wraps value in range with a yoyo (bounces at ends). Use for back-and-forth within a range.

```javascript
gsap.utils.wrapYoyo(0, 100, 150); // 50 (bounces back)
```

## Do Not

- Use **gsap.utils** for DOM queries when a simple selector or ref is enough; **toArray** is for when GSAP or your code needs a real array.
- Assume **mapRange** / **normalize** handle units; they work on numbers. Use **getUnit** / **unitize** when units matter.
- Override or rely on undocumented behavior; stick to the documented API.

### Learn More

https://gsap.com/docs/v3/HelperFunctions
