# headc — The Head Compiler

This custom coding language was made because I wanted to build apps, but to 4 different platforms on the same IDE instead of having to translate code over and over.

One source file. Four targets.

```
myapp.head  →  headc build --web      →  dist/myapp.html
            →  headc build --windows  →  dist/myapp.exe
            →  headc build --linux    →  dist/myapp.deb
            →  headc build --android  →  dist/myapp_android/
```
get it, .head -> html exe apk deb

## Install

**Requires Python 3.10+**

```sh
# Clone or download this folder, then:
python install.py

# Or manually:
pip install -e .
```

## Commands

```sh
headc run myapp.head              # Run a Head program
headc build myapp.head --web      # Build → HTML/JS
headc build myapp.head --windows  # Build → .exe  (needs PyInstaller)
headc build myapp.head --linux    # Build → .deb  (needs dpkg-deb)
headc build myapp.head --android  # Build → Gradle project
headc build myapp.head --all      # All targets
headc build myapp.head --web --out build/   # Custom output dir
headc check myapp.head            # Syntax check only
headc new myapp                   # Scaffold new project
headc version                     # Print version
```

## Build target requirements

| Target     | Extra requirement          |
|------------|---------------------------|
| `--web`    | None — pure Python        |
| `--windows`| `pip install pyinstaller` |
| `--linux`  | `dpkg-deb` on PATH        |
| `--android`| Android SDK + Gradle      |

## Language quick reference

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

## File structure

```
headc/
├── headc/
│   ├── __init__.py       version
│   ├── __main__.py       entry point
│   ├── cli.py            command dispatcher
│   ├── lexer.py          tokenizer
│   ├── parser.py         AST builder
│   ├── interpreter.py    tree-walking evaluator (headc run)
│   ├── errors.py         error types
│   ├── printer.py        colored terminal output
│   └── codegen/
│       ├── web.py        → HTML + JS
│       ├── windows.py    → .exe via PyInstaller
│       ├── linux.py      → .deb via dpkg-deb
│       └── android.py    → Gradle project
├── tests/
│   └── test.head         37-test suite (all passing)
├── install.py
├── setup.py
└── README.md
```
