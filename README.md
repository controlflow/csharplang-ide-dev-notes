# csharplang-ide-dev-notes
Attempt to collect knowledge useful for C# IDE development




# Declarations

## Local variables

### Ordinary local variables

```c#
int x = 42;
string a = "aaa", b;
```

* Participant of multiple declaration
* Multiple declaration must have explicit type
* Can have optional (array/expression) initializer
* Can be implicitly typed with `var` since C# 3.0
* Classified as a variable (can be used in `ref`/`out` argument)
* Can be declared as `ref` since C# 7.0
* Unused variables can produce compiler warnings

### Constant local variable

```c#
const int c = 42;
const SomeType Null = null;
```

* Participant of multiple declaration
* Immutable, has constant value
* Can only have explicit type annotations
* Must have expression initializer
* Can have arbitrary reference type (but only `null` as a value)
TODO: warnings?

### Foreach iteration variable

```c#
foreach (var x in xs) { … }
foreach (var (x, (y, z)) in tuples) { … }
```

* Immutable
* Can be implicitly typed with `var` since C# 3.0
* Explicit type actually means "cast" - TODO explain
* Since C# 7.0 parsed as a declaration expression, supports deconstruction
* Deconstructed variable designations are also considered "foreach iteration variables"
* Discard designations are only work inside parenthsized deconstruction (for backwards compatibility)

### Catch exception variable

```c#
try { … }
catch (Exception e) { … }
```

* Mutable, classified as a variable (can be passed as `ref`/`out` argument)
* Parsed as 
* Must be of class type, inherited from `System.Exception`

### Using statement resource variable

```c#
using (var resource = …) { … }
using (Resource r1 = …, r2 = …) { … }
```

* Participant of multiple declaration
* Multiple declaration must have explicit type
* Parsed as a part of `using` statement
* Immutable
* Must be of type that implements `System.IDisposable`

### Fixed statement pointer variable

```c#
fixed (T* pointer = …) { … }
```

* Immutable
* Parsed as a part of `fixed` statement
* Must be of pointer type
* Can only be declared in `unsafe` context

### Output argument variables

```c#
dict.TryGetValue(key, out var value)
```

* Represented in syntax tree via "variable designation"
* Parsed as a declaration expression with designation, only in `out` arguments
* Mutable, classified as a variable (can be passed as `ref`/`out` argument)
* Can be implicitly typed with `var`
* Implicit type is received from containing invocation overload resolution results

### Deconstruction variables

```c#
var (a, b) = …;
(var c, var d) = …;
(string e, (int f, _)) = …;
```

* Represented in syntax tree via "variable designation" ("`a`")
* Designations are parsed inside "parenthsized designation" ("`(a, b)`") of declaration expression ("`var (a, b)`")
* Designations also are parsed in declaration expressions "`var c`" in tuple literal arguments `(var c, …)`
* Both tuple literals and parenthsized designations can be nested
* Mutable, classified as a variable (can be passed as `ref`/`out` argument)
* Can be implicitly typed with `var`
* Parenthsized designation version (`var (a, b)`) can't declare type explicitly
* Implicit type is received from assignment source expression type (from tuple type or `Deconstruct()` method lookup and checking corresponding `out` parameter type)








