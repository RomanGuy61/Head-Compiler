!MORE WILL BE ADDED LATER!

```head
-- Comments start with --

app MyApp:
    title: "My App"

    -- Typed state variables
    state:
        count: int = 0
        name:  str = ""
        items: list<str> = []

    -- Functions
    fn greet(who: str):
        print("Hello, " + who + "!")

    fn factorial(n: int):
        if n <= 1:
            return 1
        return n * factorial(n - 1)

    -- Control flow
    if count > 0:
        print("positive")
    elif count < 0:
        print("negative")
    else:
        print("zero")

    -- Loops
    each item, i in items:
        print(str(i) + ": " + item)

    while count < 10:
        count = count + 1

    -- Inline typed vars
    total: int = 0

    -- Built-in functions
    print(len(items))
    print(str(42))
    print(abs(-5))
    print(max([1, 2, 3]))
    print(range(10))

    greet("World")
```
