---
title: mapOutput.ts
nav_order: 17
parent: Modules
---

---

<h2 class="text-delta">Table of contents</h2>

- [mapOutput (function)](#mapoutput-function)

---

# mapOutput (function)

Changes the output type of the given runtime type

**Signature**

```ts
export const mapOutput = <A, O, I, P>(codec: Type<A, O, I>, f: (p: O) => P, name?: string): Type<A, P, I> =>
  new Type(name === undefined ? codec.name : name, codec.is, codec.validate, a => ...
```

**Example**

```ts
import * as t from 'io-ts'
import { mapOutput } from 'io-ts-types/lib/mapOutput'
import { createOptionFromNullable } from 'io-ts-types/lib/fp-ts/createOptionFromNullable'
import { none, some } from 'fp-ts/lib/Option'

// Input: t.Type<Option<number>, number | null, t.mixed>
const Input = createOptionFromNullable(t.number)

const toUndefined = <A>(x: A | null): A | undefined => (x === null ? undefined : x)

// Output: t.Type<Option<number>, number | undefined, t.mixed>
const Output = mapOutput(Input, toUndefined)

assert.strictEqual(Output.encode(none), undefined)
assert.strictEqual(Output.encode(some(1)), 1)
```