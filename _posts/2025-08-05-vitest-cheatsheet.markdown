---
layout: post
title: "vitest cheatsheet"
date: 2025-08-05 01:38:00 +0800
categories: vitest
math: true
---

# Vitest Cheatsheet
> [Vitest Documentation](https://vitest.dev/guide/)

## Installing vitest

```bash
npm install -D vitest
```

Boom, now you can use it on any react app, you actually dont even need vite! (might have a few extra steps to setup)

For my github repo, I created a basic react vite app using `pnpm create vite`. You can do the same, then install vitest.

```bash
pnpm create vite

// ...

pnpm add -D vitest
```

## Getting started
To start using vitest, create a <name>.spec.ts/tsx or <name>.test.ts/tsx file with the same name as the file you want to test.

### Using test/it from vitest
```typescript
// sum.spec.ts
import { expect, test, it } from "vitest"
import { sum } from "./sum"

it("Test sum" , () => {
	expect(sum(1, 2)).toBe(3)
});

// sum.ts
export function sum(a: number, b: number) {
	return a + b;
}
```

The expect() function is basically running the sum() function with 1, 2 as the args and comparing that value to the .toBe(3) that we have set as the expected value. The convention is to do expect() followed by the toBe() or to<insertName>()

### Grouping tests using describe

```typescript
// sum.spec.ts
import { describe, expect, it } from "vitest"
import { sum } from "./sum"

describe("basic sum usage", () => {
    it("Test sum", () => {
        expect(sum(1, 2)).toBe(3);
    });
});

describe("advanced sum usage", () => {
    it("Advanced test sum", () => {
        expect(sum(1, 2)).toBe(3);
    });
});
```

```console
✓ src/utils/sum.spec.ts (2 tests) 7ms
   ✓ basic sum usage > Test sum 3ms
   ✓ advanced sum usage > Advanced test sum 1ms

 Test Files  1 passed (1)
      Tests  2 passed (2)
   Start at  23:28:11
   Duration  55ms
```
