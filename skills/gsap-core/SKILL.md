---
name: gsap-core
description: Use GSAP core API correctly — gsap.to(), gsap.from(), gsap.fromTo(), easing, duration, stagger, and defaults. Use when animating DOM elements, SVG, or objects with GSAP, or when the user asks about GSAP tweens, easing, or basic animation.
license: MIT
---

# GSAP Core

## When to Use This Skill

Apply when writing or reviewing GSAP animations that use the core engine: single tweens, eases, staggers, or when explaining how GSAP tweens work.

## Core Tween Methods

- **gsap.to(targets, vars)** — animate from current state to `vars`. Most common.
- **gsap.from(targets, vars)** — animate from `vars` to current state (good for entrances).
- **gsap.fromTo(targets, fromVars, toVars)** — explicit start and end; no reading of current values.
- **gsap.set(targets, vars)** — apply immediately (duration 0).

Always use **property names in camelCase** in the vars object (e.g. `backgroundColor`, `marginTop`, `rotationX`, `scaleY`).

## Common vars

- **duration** — seconds (default 0.5).
- **delay** — seconds before start.
- **ease** — string or function. Prefer built-in: `"power1.out"` (default), `"power3.inOut"`, `"back.out(1.7)"`, `"elastic.out(1, 0.3)"`, `"none"`.
- **stagger** — number (seconds between) like `0.1` or object: `{ amount: 0.3, from: "center" }`, `{ each: 0.1, from: "random" }`.
- **overwrite** — `false` (default), `true` (immediately kill all active tweens of the same targets), or `"auto"` (when the tween renders for the first time, only kill individual overlapping properties in other **active** tweens of the same targets).
- **repeat** — number or `-1` for infinite.
- **yoyo** — boolean; with repeat, alternates direction.
- **onComplete**, **onStart**, **onUpdate** — callbacks; scoped to the Animation instance itself (Tween or Timeline).

## Targets

- **Single or Multiple**: CSS selector string, element reference, array or NodeList. GSAP handles arrays; use stagger for offset.

## Stagger

Offset the animation of each item by 0.1 second like this: 
```javascript 
gsap.to(".item", {
  y: -20,
  stagger: 0.1
});
```
Or use the object syntax for advanced options like how each successive stagger amount is applied to the targets array (`from: "random" | "start" | "center" | "end" | "edges" | (index)`)

### Learn More

https://gsap.com/resources/getting-started/Staggers

## Easing

Use string eases unless a custom curve is needed:

```javascript
ease: "power1.out"     // default feel
ease: "power3.inOut"
ease: "back.out(1.7)"  // overshoot
ease: "elastic.out(1, 0.3)"
ease: "none"           // linear
```

Built-in eases: base (same as `.out`), `.in`, `.out`, `.inOut` where "power" refers to the strength of the curve (1 is more gradual, 4 is steepest):

```
base (out)        .in                .out               .inOut
"none"
"power1"          "power1.in"        "power1.out"       "power1.inOut"
"power2"          "power2.in"        "power2.out"       "power2.inOut"
"power3"          "power3.in"        "power3.out"       "power3.inOut"
"power4"          "power4.in"        "power4.out"       "power4.inOut"
"back"            "back.in"          "back.out"         "back.inOut"
"bounce"          "bounce.in"        "bounce.out"      "bounce.inOut"
"circ"            "circ.in"          "circ.out"        "circ.inOut"
"elastic"         "elastic.in"       "elastic.out"     "elastic.inOut"
"expo"            "expo.in"          "expo.out"        "expo.inOut"
"sine"            "sine.in"          "sine.out"        "sine.inOut"
```

### Custom: use CustomEase (plugin)

Simple cubic-bezier values (as used in CSS `cubic-bezier()`): 

```javascript
const myEase = CustomEase.create("my-ease", ".17,.67,.83,.67");

gsap.to(".item", {x: 100, ease: myEase, duration: 1});
```

Complex curve with any number of control points, described as normalized SVG path data: 

```javascript
const myEase = CustomEase.create("hop", "M0,0 C0,0 0.056,0.442 0.175,0.442 0.294,0.442 0.332,0 0.332,0 0.332,0 0.414,1 0.671,1 0.991,1 1,0 1,0");

gsap.to(".item", {x: 100, ease: myEase, duration: 1});
```

## Returning and Controlling Tweens

All tween methods return a **Tween** instance. Store the return value when controlling playback is needed:

```javascript
const tween = gsap.to(".box", { x: 100, duration: 1, repeat: 1, yoyo: true });
tween.pause();
tween.play();
tween.reverse();
tween.kill();
tween.progress(0.5);
tween.time(0.2);
tween.totalTime(1.5);
```

## Function-based values
Use a function for a `vars` value and it will get called **once for each target** the first time the tween renders, and whatever is returned by that function will be used as the animation value.

```javascript
gsap.to(".item", {
  x: (i, target, targetsArray) => i * 50, // first item animates to 0, the second to 50, the third to 100, etc.
  stagger: 0.1
});
```

## Relative values

Use a `+=`, `-=`, `*=`, or `/=` prefix to indicate a **relative** value. For example, the following will animate x to 20 pixels less than whatever it is when the tween renders for the first time.

```javascript
gsap.to(".class", {x: "-=20" });
```
`x: "+=20"` would add 20 to the current value. `"*=2"` would multiply by 2, and `"/=2"` would divide by 2.


## Defaults

Set project-wide Tween defaults with **gsap.defaults()**:

```javascript
gsap.defaults({ duration: 0.6, ease: "power2.out" });
```

## Do Not

- Animate layout-heavy properties (e.g. `width`, `height`, `top`, `left`) when **transform** properties (`x`, `y`, `scaleX`, `scaleY`, `rotation`) can achieve the same effect; prefer transforms for better performance.
- Use invalid or non-existent ease names; stick to documented eases.
- Forget that **gsap.from()** uses the element’s current state as the end state; the initial values in the tween will be applied immediately unless `immediateRender: false` is in the `vars`.
