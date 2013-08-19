Main items like repo names, folders, and classes are in [PascalCase](http://c2.com/cgi/wiki?PascalCase).

Lesser items like class properties and variables are in [camelCase](http://msdn.microsoft.com/en-us/library/x2dbyw72.aspx).

The Sesame namespace is `SME`, used for all Cocoa, Pytnon, and JavaScript/CoffeeScript global objects.

Indent using 4 spaces. Never indent with tabs.

# Git

## Repos

Get repositories are pascal-case and namespaced with `Sesame`.

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

## Variables

Variables should be named as descriptively as possible. Single letter variable names should be avoided except in `for()` loops.

Asterisks indicating pointers belong with the variable, e.g., `NSString *text` not `NSString* text` or `NSString * text`, except in the case of constants.

Property definitions should be used in place of naked instance variables whenever possible. Direct instance variable access should be avoided except in initializer methods (`init`, `initWithCoder:`, etc…), `dealloc` methods and within custom setters and getters. For more information on using Accessor Methods in Initializer Methods and dealloc, see [here](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/MemoryMgmt/Articles/mmPractical.html#//apple_ref/doc/uid/TP40004447-SW6).

**For example:**

```objc
@interface SMEUser: NSObject

@property (strong, nonatomic) NSString *name;

@end
```

**Not:**

```objc
@interface SMEUser : NSObject {
    NSString *name;
}
```

## Methods

In method signatures, there should be a space after the scope (-/+ symbol). There should be a space between the method segments.

**For Example**:
```objc
- (void)setExampleText:(NSString *)text image:(UIImage *)image;
```

## Naming

Apple naming conventions should be adhered to wherever possible, especially those related to [memory management rules](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/MemoryMgmt/Articles/MemoryMgmt.html) ([NARC](http://stackoverflow.com/a/2865194/340508)).

Long, descriptive method and variable names are good.

**For example:**

```objc
UIButton *settingsButton;
```

**Not**

```objc
UIButton *setBut;
```

A three letter prefix (e.g. `SME`) should always be used for class names and constants. 
Constants should be camel-case with all words capitalized and prefixed by the related class name for clarity.

**For example:**

```objc
static const NSTimeInterval NYTArticleViewControllerNavigationFadeAnimationDuration = 0.3;
```

**Not:**

```objc
static const NSTimeInterval fadetime = 1.7;
```

Properties should be camel-case with the leading word being lowercase. 
**If Xcode can automatically synthesize the variable, then let it.** 
Otherwise, in order to be consistent, the backing instance variables for these properties should be camel-case with the leading word being lowercase and a leading underscore. 
This is the same format as Xcode's default synthesis.

**For example:**

```objc
@synthesize descriptiveVariableName = _descriptiveVariableName;
```
