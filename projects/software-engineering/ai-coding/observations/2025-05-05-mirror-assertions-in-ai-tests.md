---
title: Mirror assertions in AI-generated unit tests
created: 2025-05-05
updated: 2025-11-22
tags: [observation, ai, testing, assertions]
status: draft
summary: AI-generated tests often recompute expected values by calling the same helpers as production code, which hides bugs instead of detecting them.
---

# Context

In many AI-generated unit tests, the agent builds the expected value by calling the same helpers or pure functions that production code uses. This creates a mirror of the implementation instead of an independent check.

# Content

Example pattern:

```js
export function translatePoint(point, offset) {
  return multiplyMatrix(buildTranslationMatrix(offset), point);
}

test('translatePoint moves the point', () => {
  const point = [1, 2, 3, 1];
  const offset = [0, 5, -2, 0];
  const result = translatePoint(point, offset);

  // Mirror assertion anti-pattern:
  // The test recomputes the expected value with the same helpers.
  const expected = multiplyMatrix(buildTranslationMatrix(offset), point);
  expect(result).toEqual(expected);
});
```

Why this is a problem:

- The test shares logic with the implementation. If there is a bug in `multiplyMatrix` or `buildTranslationMatrix`, the same bug appears on both sides of the assertion.
- The test does not describe observable behaviour. It only checks that two uses of the same logic produce the same output.
- The test gives a false sense of safety, because it can still pass when the core computation is wrong.

Better pattern:

- Use a trusted fixture or a hand-calculated expected value that does not call the same helpers as production code.
- Keep assertions focused on observable behaviour and domain-level expectations, not on repeating internal implementation steps.

For the example above, a better assertion would be:

```js
expect(result).toEqual([1, 7, 1, 1]);
```

This forces the test to fail if there is a defect in `multiplyMatrix` or `buildTranslationMatrix`.

# Next Steps

- Collect more examples of mirror assertions in AI-generated tests across different languages and frameworks.
- See how often this pattern appears when the prompt does not explicitly request concrete expected values.
- Experiment with prompts that explicitly ask for hand-written expected values or fixtures instead of recomputing results through the same helpers.
