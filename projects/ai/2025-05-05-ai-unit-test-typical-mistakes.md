---
created: 2025-05-05
updated: 2025-10-16
topic: typical AI unit test mistakes
tags: [testing, ai, quality]
---

# Catalog: Typical AI Mistakes in Unit Tests

I want a running list of the recurring patterns I see in AI-generated unit tests that end up weakening coverage or producing false confidence.

## Mirror assertions 

The test reuses the same helper or pure function that the production code calls to build the expected value, so any bug in that helper appears in both places and the test still passes.  

```js
export function translatePoint(point, offset) {
  return multiplyMatrix(buildTranslationMatrix(offset), point);
}

test('translatePoint moves the point', () => {
  const point = [1, 2, 3, 1];
  const offset = [0, 5, -2, 0];
  const result = translatePoint(point, offset);
  // AI anti-pattern: recompute with the same helpers as production.
  const expected = multiplyMatrix(buildTranslationMatrix(offset), point);
  expect(result).toEqual(expected);
});
```

Better: compare against a trusted fixture so a bug in `multiplyMatrix` cannot hide (`expect(result).toEqual([1, 7, 1, 1])`).