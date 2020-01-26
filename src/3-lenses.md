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

### Record part 2


## 4. Limitations

For each type signature, give a valid lens definition (if possible)!
If not, explain why. Can you impose additional constraints to make a (potentially law-less) definition? 

1. `second :: Lens' (a,b,c) b`

    ```haskell
    second = _2
    ```

2. `inMaybe :: Lens' (Maybe a) a`

    No, there's no way to retrieve an `a` out of `Nothing`. But suppose we had this instead:

    ```haskell
    inMaybe :: Monoid a => Lens' (Maybe a) a
    inMaybe = lens getMaybe setMaybe
        where getMaybe (Just a) = a
              getMaybe Nothing = mempty
              setMaybe (Just _) a = Just a
              setMaybe Nothing _ = Nothing
    ```

    We basically swap `Nothing` with unchangable `mempty`.
    However, note that this definition does not satisfy `view inMaybe (set inMaybe a m) == a` 

3. `left :: Lens' (Either a b) a`

    In the general case, no since we can't retrieve an `a` from `Right b`.
    However, if we have `Either a a`, then we can define the following:

    ```haskell
    chosen :: Lens' (Either a a) a
    chosen = lens getEither setEither
        where getEither (Left a) = a
              getEither (Right a) = a
              setEither (Left _) a = Left a
              setEither (Right _) a = Right a
    ```

4. `listThird :: Lens' [a] a`

    No, same issue as `Maybe`...can't retrieve `a` from `[]`. 
    Suppose we had this instead:

    ```haskell
        data NonEmpty a = a :| [a]

        listFirst :: Lens' (NonEmpty a) a
        listFirst = lens getFirst setFirst
            where getFirst (a :| _) = a
                  setFirst (_ :| as) a = a :| as
    ```

    Clearly, this works because we're guaranteed at least one element.

5. `condtional :: Lens' (Bool, a, a) a` where the focus is based on the `Bool` value

    ```haskell
    conditional = lens getCond setCond
        where getCond (True, a, _) = a
              getCond (False, _, a) = a
              setCond (True _, a) a' = (True, a', a)
              setCond (False, a, _) a' = (False, a, a')
    ```

6. `msg :: Lens' Err String` where `data Err = Exception { _msg :: String } | ExitCode { _code :: Int }`

    Clearly, the tricky part is dealing with `ExitCode`. 

    You might be tempted to convert `_code` to a `String`. This fulfills the get, but since
    not every `String` represents a valid `Int`, this does not work.

    The other option is to apply our `Monoid` trick, where `mempty = ""`. But what if we
    had some non-monoidal type instead of `String`? Well, if the type contains at least one
    value, we can use that.

    ```haskell
    msg = lens getMsg setMsg
        where getMsg (Exception m) = m
              getMsg (ExitCode _) = ""
              setMsg (Exception _) m = Exception m
              setMsg (ExitCode c) _ = ExitCode c
    ```
    
    We could also combine the two approached together, though I'm not sure what that buys you.


