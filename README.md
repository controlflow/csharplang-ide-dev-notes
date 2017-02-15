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
const SomeType Null = null;
```

* Immutable, has constant value
* Can only have explicit type annotations
* Must have expression initializer
* Can have arbitrary reference type (but only `null` as a value)

### Foreach iteration variable

```c#
foreach (var x in xs) { … }
foreach (var (x, (y, z)) in tuples) { … }
```

* Immutable
* Can be implicitly typed with `var` since C# 3.0
* Since C# 7.0 parsed as a declaration expression, supports deconstruction
* Deconstructed variable designations are also considered "foreach iteration variables"
* Discard designations are only work inside parenthsized deconstruction (for backwards compatibility)

### Catch exception variable

```c#
try { … }
catch (Exception e) { … }
```

* Mutable, classified as a variable (can be passed as `ref`/`out` argument)
* Must be of class type, inherited from `System.Exception`

### Using statement resource variable

```c#
using (var resource = …) { … }
```

* Immutable
* Must be of type that implements `System.IDisposable`

### 













