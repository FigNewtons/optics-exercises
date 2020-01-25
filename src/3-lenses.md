# 3 - Lenses

## 1. Optic anatomy

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

## 2. Lens Actions

1. Name the structure and focus of this lens: `Lens' (Bool, (Int, String)) Int`.
  - __structure:__ `(Bool, (Int, String))`
  - __focus:__ `Int`

2. Write a (simplified) type signature of a Lens with structure `(Char, Int)` and focus `Char`.

    `Lens' (Char, Int) Char`

3. Name three actions we can use on a Lens.

    __view, set, over__

4. Which lens could I use to focus on `'c'` in `('a','b','c')`?

    `_3`

5. Write out the (simplified) types of each part in the expression: 

    `over _2 (*10) (False, 2)`

    What does it evaulate to?

    ```haskell
    over :: Lens' (Bool, Int) Int -> (Int -> Int) -> (Bool, Int) -> (Bool, Int)
    _2 :: Lens' (Bool, Int) Int
    (*10) :: Int -> Int
    (False, 2) :: (Bool, Int)
    ```
    __Result:__ `(False,20)`

## 3. Lenses and Records

### Records part 1

1. What letters are used to denote the structure and focus of a lens, respectively?
  - __structure:__ `s`
  - __focus:__ `a`

2. Which two components are required to create a lens?
    getter `(s -> a)` and setter `(s -> a -> s)` methods

3. Given the following record, 

    ```haskell
        data Ship = Ship { _name :: String, _numCrew :: Int }
    ```

    implement a lens for the `_name` field.

    ```haskell
        name :: Lens' Ship String
        name = lens _name (\s n -> s { _name = n })
    ```




