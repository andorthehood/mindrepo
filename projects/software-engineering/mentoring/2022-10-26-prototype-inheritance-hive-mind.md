---
title: Prototype inheritance (hive-mind metaphor)
created: 2022-10-26
updated: 2025-12-14
tags: [javascript, mentoring, prototypes, metaphor]
status: draft
summary: A metaphor I used to explain JavaScript prototype inheritance and prototype chains to a junior developer, including both values and functions.
---

# Context
I once explained JavaScript prototype inheritance to a junior developer using a hive-mind metaphor. This note records that explanation so I can reuse it.

# Content
## Mental model
- Each object is an individual “drone” with its own local knowledge (its own properties).
- Each object has a link to a “shared mind” (its prototype).
- That shared mind can link to a higher shared mind (the prototype chain).

## How property lookup works (reads)
When you access `obj.someThing`, JavaScript checks:
1) Does `obj` have an own property named `someThing`?
2) If not, does `obj`’s prototype have `someThing`?
3) If not, does the next prototype up the chain have it?
This continues until the property is found or the prototype is `null`.

In the metaphor: the drone checks its own memory first, then consults the hive mind, then higher levels of the hive mind.

## Values, not just functions
Prototype properties can be any value, not just methods: numbers, strings, objects, arrays, booleans, and functions. The lookup rules are the same.

Example (value + shadowing):
```js
const proto = { kind: "worker", level: 1 };
const obj = Object.create(proto);

obj.kind;      // "worker" (from proto)
obj.kind = "scout";
obj.kind;      // "scout" (own value shadows proto)
```

## How assignment works (writes)
When you do `obj.someThing = value`, JavaScript generally creates or updates an own property on `obj`.

In the metaphor: you taught that one drone something new; you did not update the hive mind.

Important exception: if a setter exists somewhere on the prototype chain for `someThing`, that setter can run instead of creating an own property.

## Shadowing
If the prototype provides `someThing` but the object later gets its own `someThing`, the own property “wins” during lookup.

In the metaphor: the drone’s local memory overrides what it would otherwise get from the hive mind.

## Shared reference pitfall (prototype provides an object)
If the prototype provides an object value, multiple objects can share the same underlying object reference.

In the metaphor: the hive mind is holding a single shared notebook; all drones read and write to the same notebook unless they get their own copy.

Example (shared reference):
```js
const proto = { settings: { debug: false } };
const a = Object.create(proto);
const b = Object.create(proto);

a.settings.debug = true;
b.settings.debug; // true (same shared object reference)
```

## How `new` fits
When you do `new Constructor()`, JavaScript creates a new object whose prototype link starts at `Constructor.prototype`.

In the metaphor: `Constructor.prototype` is the shared mind for objects created by that constructor.