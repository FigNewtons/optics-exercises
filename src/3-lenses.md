# Lenses

## Optic anatomy

1. `view (_1 . _2) ((1,2),3)`
  - action: `view`
  - path: `(_1 . _2)`
  - structure: `((1,2),3)`
  - focus: `2`

2. `set (_2 . _Left) "new" (False, Left "old")`
  - action: `set`
  - path: `(_2 . _Left)`
  - structure: `(False, Left "old")`
  - focus: `"old"`

3. `over (taking 2 worded . traversed) toUpper "testing one two three"`
  - action: `over`
  - path: `(taking 2 worded . traversed)`
  - structure: `"testing one two three"`
  - focus: `"testing one"`

4. `foldOf (both . each) (["super", "cali"], ["fragilistic", "expialidocious"])`
  - action: `foldOf`
  - path: `(both . each)`
  - structure: `(["super", "cali"], ["fragilistic", "expialidocious"])`
  - focus: `"super", "cali", "fragilistic", "expialidocious"`
