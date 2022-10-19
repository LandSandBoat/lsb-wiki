# Development Guide (C++)

## Naming & Misc

- The STL is your friend, don't be afraid to use it.
- Be careful with `auto`, it can mask important type details.
- Be as `const` as you reasonably can.
- `UpperCamelCase` for namespaced functions and classes.
- `UPPER_SNAKE_CASE` for enums (exception for enum classes: style as classes).
- `lowerCamelCase` for everything else.

## Styling

We keep a `.clang-format` file in the root of the repo, but accept it can be difficult to set up for use on _just your changes_, as opposed to entire files that you're working with that might have legacy styling you don't want to mess with.

Here are the points from `.clang-format` explained:

#### BasedOnStyle: WebKit

When in doubt, defaulting to `WebKit style with Allman braces` is _seemingly_ a safe option.

#### AccessModifierOffset: -4

```cpp
// Correct ✔️ 
class Classname
{
public:
    Classname();

private:
    int member;
}

// Wrong ❌
class Classname
{
    public:
    Classname();

    private:
    int member;
}
```

#### AllowShortFunctionsOnASingleLine: Empty

```cpp
// Correct ✔️ 
void f()
{ 
    foo(); 
}

// Wrong ❌
void f() { foo(); }
```

#### BreakBeforeBraces: Allman

Braces should _almost always_ be on a new line.

```cpp
// Correct ✔️ 
if (x == 5)
{
    function();
}

// Wrong ❌
if (x == 5) {
    function();
}
```

#### BreakConstructorInitializers: BeforeComma & ConstructorInitializerIndentWidth: 0

```cpp
// Correct ✔️ 
Constructor(int param0, int param1)
: member0(param0)
, member1(param1)
{
}

// Wrong ❌
Constructor(int param0, int param1)
    : member0(param0), member1(param1){}
```

#### CompactNamespaces: 'false'

```cpp
// Correct ✔️ 
namespace Foo
{
    namespace Bar
    {
    }
}

// Wrong ❌
namespace Foo { namespace Bar {
}}
```

#### Cpp11BracedListStyle: 'false'

```cpp
// Correct ✔️ 
std::vector<int> x{ 1, 2, 3, 4 };

// Wrong ❌
std::vector<int> x{1, 2, 3, 4};
```

#### IndentCaseLabels: 'true'

```cpp
// Correct ✔️ 
switch(x)
{
    case 0:
    {
        break;
    }  
}

// Wrong ❌
switch(x)
{
case 0:
{
    break;
}  
}
```

- **Note**: It doesn't matter if your `break;` is inside or outside the body of your case statement - as long as it's there (if you indend it to be).

#### IndentWidth: 4

```cpp
// Correct ✔️ 
if (func())
{
    reaction();  
}

// Wrong ❌
if (func())
{
  reaction();  
}
```

#### KeepEmptyLinesAtTheStartOfBlocks: 'false'

```cpp
// Correct ✔️ 
void function(int x)
{
    doSomething(x);
}

// Wrong ❌
void function(int x)
{

    doSomething(x);
}
```

#### Language: Cpp

Yup.

#### PointerAlignment: Left

```cpp
// Correct ✔️ 
void function(CBigType* type);
void function(CBigType& type);

// Wrong ❌
void function(CBigType *type);
void function(CBigType &type);

// Wrong ❌
void function(CBigType * type);
void function(CBigType & type);
```

#### SortIncludes: 'true' & SortUsingDeclarations: 'true'

- Try to keep your `include` and `using` statements organised alphabetically, in logical blocks.

#### SpaceBeforeParens: ControlStatements

```cpp
// Correct ✔️ 
if (true)
{
    doThing();
}

// Wrong ❌
if(true)
{
    doThing();
}
```

#### Standard: Cpp11

```cpp
// Correct ✔️ 
A<A<int>>

// Wrong ❌
A<A<int> >
```

#### UseTab: Never

```cpp
// Correct ✔️
<4 spaces>

// Wrong ❌
<a tab>

// Wrong ❌
<a half-tab>
```

#### Braces Around Statements

`readability-braces-around-statements`

```cpp
// Correct ✔️ 
if (x == 5)
{
    function();
}

// Wrong ❌
if (x == 5)
    function();

// Wrong ❌
if (x == 5)
    function(21);
else
{
    function(42);
}
```

#### Breaks between consecutive conditional statements

```cpp
// Correct ✔️ 
if (thisThing())
{

}
else
{

}

if (thatThing())
{

}

// Correct ✔️ 
if (thisThing())
{

}

if (thatThing())
{

}

// Wrong ❌
if (thisThing())
{

}
else
{

}
if (thatThing())
{

}

// Wrong ❌
if (thisThing())
{

}
if (thatThing())
{

}
```

#### Casting - static_cast over C-Style

`cppcoreguidelines-pro-type-cstyle-cast`

```cpp
// Correct ✔️ 
uint32 param = static_cast<uint32>(input);

// Wrong ❌
uint32 param = (uint32)input;
```

#### Don't use static_cast to downcast: Use dynamic_cast instead

`cppcoreguidelines-pro-type-static-cast-downcast`

**NOTE**: There is a good reason for this. If you use `static_cast` and it fails, the returned pointer will **NOT NECESSARILY** be `nullptr` and any blocks checking against for `nullptr` might incorrectly succeed. `dynamic_cast` will return a `nullptr` if it fails.

```cpp
// Correct ✔️ 
if (auto PChar = dynamic_cast<CCharEntity*>(baseEntity))
{
    PChar->DoSomething()
}

// Wrong ❌
auto PChar = static_cast<CCharEntity*>(baseEntity)
PChar->DoSomething()

// Wrong ❌
if (auto PChar = static_cast<CCharEntity*>(baseEntity))
{   
    // The cast is forced, so PChar will _always_ be populated here....
    PChar->DoSomething()
}
```

#### Arg/Param spacing

```cpp
// Correct ✔️ 
auto f(0, 1, 2, 3, 4, 5, 6);

// Wrong ❌
auto f(0,1,2,3,4,5,6);
```

#### Lambdas

Formatting tools have a famously difficult time with lamdas, so we tend to wrap them in `// clang-format on/off` to ensure we can format them how we'd like.

```cpp
// Correct ✔️ 
// clang-format off
auto isEntityAlive = [&](CBigEntity* entity) -> bool
{
    return entity->isAlive;
};
// clang-format on

// Correct ✔️ 
// clang-format off
static_cast<CCharEntity>(PPlayer)->ForParty([&](CBattleEntity* entity)
{
    entity->doStuff();
});
// clang-format off

// Wrong ❌
auto isEntityAlive =
[&](CBigEntity* entity)
    {
        return entity->isAlive;
    };
```
