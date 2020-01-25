# Lenses

## Optic anatomy

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
