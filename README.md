# csharplang-ide-dev-notes
Attempt to collect knowledge useful for C# IDE development




# Declarations

## Local variables

### Ordinary local variables

```c#
int x = 42;
```

* Can have (array/expression) initializer
* Can be implicitly typed with `var` since C# 3.0
* Classified as a variable (can be used in `ref`/`out` argument)
* Can be declared as `ref` since C# 7.0

### Constant local variable

```c#
const int c = 42;
```

### Foreach iteration variable

```c#
foreach (var x in xs) { … }
```

* Immutable

### Using statement resource variable

```c#
using (var resource = …)
```

* Immutable

### 