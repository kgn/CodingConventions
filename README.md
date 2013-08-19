Main items like repo names, folders, and classes are in [PascalCase](http://c2.com/cgi/wiki?PascalCase).

Lesser items like class properties and variables are in [camelCase](http://msdn.microsoft.com/en-us/library/x2dbyw72.aspx).

The Sesame namespace is `SME`, used for all Cocoa, Pytnon, and JavaScript/CoffeeScript global objects.

Indent using 4 spaces. Never indent with tabs.

# Git

## Repos

Get repositories are Pascal Case and namespaced with `Sesame`.

Examples `SesameCocoa`, `SesameWebsite`.

## Branches

Git branches are grouped together by the `/` seperator so they are organized into *directories* in GUI apps.

There are currently two groups:
- `feature` - A feature branch. Examples: `feature/sound-control`, `feature/x-ray`
- `build` - A build branch for the build system. Examples: `build/release`, `build/beta`.

# C Based Syntex Languages

Method braces and other braces (`if`/`else`/`switch`/`while` etc.) always open on the same line as the statement but close on a new line.
There should be no space around the braces to make the code more compact.

**For example:**
```objc
if(user.isHappy){
    //Do something
}else{
    //Do something else
}
```

## Conditionals

Conditional bodies should always use braces even when a conditional body could be written without braces (e.g., it is one line only) to prevent [errors](https://github.com/NYTimes/objective-c-style-guide/issues/26#issuecomment-22074256). These errors include adding a second line and expecting it to be part of the if-statement. Another, [even more dangerous defect](http://programmers.stackexchange.com/a/16530) may happen where the line "inside" the if-statement is commented out, and the next line unwittingly becomes part of the if-statement. In addition, this style is more consistent with all other conditionals, and therefore more easily scannable.

**For example:**
```objc
if(!error){
    return success;
}
```

**Not:**
```objc
if (!error)
    return success;
```

or

```objc
if (!error) return success;
```

### Ternary Operator

The Ternary operator, ? , should only be used when it increases clarity or code neatness. A single condition is usually all that should be evaluated. Evaluating multiple conditions is usually more understandable as an if statement, or refactored into instance variables.

**For example:**
```objc
result = a > b ? x : y;
```

**Not:**
```objc
result = a > b ? x = c > d ? c : d : y;
```


# Objective-C

## Dot Notation

Avoid mixing square brackets and dots.

**For example:**
```objc
[[UIApplication sharedApplication] delegate];
```
or
```
UIApplication *app = [UIApplication sharedApplication];
app.delegate;
```

**Not:**
```objc
[UIApplication sharedApplication].delegate;
```
or
```
UIApplication.sharedApplication.delegate;
```
