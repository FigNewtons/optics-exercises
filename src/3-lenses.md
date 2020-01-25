# Lenses

## Optic anatomy

For each expression, identify the action, path, structure and focus.

1. `view (_1 . _2) ((1,2),3)`
  - __action:__ `view`
  - __path:__ `(_1 . _2)`
  - __structure:__ `((1,2),3)`
  - __focus:__ `2`

2. `set (_2 . _Left) "new" (False, Left "old")`
  - __action:__ `set`
  - __path:__ `(_2 . _Left)`
  - __structure:__ `(False, Left "old")`
  - __focus:__ `"old"`

3. `over (taking 2 worded . traversed) toUpper "testing one two three"`
  - __action:__ `over`
  - __path:__ `(taking 2 worded . traversed)`
  - __structure:__ `"testing one two three"`
  - __focus:__ `"testing one"`

4. `foldOf (both . each) (["super", "cali"], ["fragilistic", "expialidocious"])`
  - __action:__ `foldOf`
  - __path:__ `(both . each)`
  - __structure:__ `(["super", "cali"], ["fragilistic", "expialidocious"])`
  - __focus:__ `"super", "cali", "fragilistic", "expialidocious"`

## Lens Actions

1. Name the structure and focus of this lens: `Lens' (Bool, (Int, String)) Int`

2. Write a (simplified) type signature of a Lens with structure `(Char, Int)` and focus `Char`

3. Name three actions we can use on a Lens.

4. Which lens could I use to focus on `c` in `('a','b','c')`?

5. Write out the (simplified) types of each part in the expression: 

    `over _2 (*10) (False, 2)`

    What does it evaulate to?

