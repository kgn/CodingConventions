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

## Comments

Comments should be used sparingly due to the self documenting nature of Objective-C.
Comments should be used to explain **why** a particular piece of code does something. 
Any comments that are used must be kept up-to-date or deleted.

There should always be a space after the `//`.
**For example:**
```objc
// This is where we do the thing
```

Block comments should generally be avoided, as code should be as self-documenting as possible, 
with only the need for intermittent, few-line explanations. 
This does not apply to comments that are used to generate documentation.

### TODO

The `// TODO:` comment is encuraged to make notes of what is needed to be done. 
As soon as a todo is complete the comment should be deleted.

**For example:**
```objc
// TODO: Still have to add threading
```

### HACK

The `// HACK:` comment should be used to flag a particually hacky peice of code that is working but should probaly be fixed in the future.

**For example:**
```objc
// HACK: Not sure why 5px needs to be added here but it's working
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
static const NSTimeInterval SMEPhotoViewControllerFadeAnimationDuration = 0.3;
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

### Underscores

When using properties, instance variables should always be accessed and mutated using `self.`. 
This means that all properties will be visually distinct, as they will all be prefaced with `self.`. 
Local variables should not contain underscores.

## init and dealloc

`dealloc` methods should be placed at the top of the implementation, 
directly after the `@synthesize` and `@dynamic` statements. 
`init` should be placed directly below the `dealloc` methods of any class.

`instancetype` should always be used for `init` and class methods that return the initialized object.

`init` methods should be structured like this:

```objc
- (instancetype)init{
    self = [super init];
    if(self){
        // Custom initialization
    }
    return self;
}
```

Helper class methods are prefered for creating custom object.

**For example:**

```objc
+ (instancetype)photoViewControllerWithPhoto:(SMEPhoto *)photo andDelegate:(id<SMEPhotoViewControllerDelegate>)delegate;
```

## Literals

`NSString`, `NSDictionary`, `NSArray`, and `NSNumber` literals should be used whenever creating immutable instances of those objects. Pay special care that `nil` values not be passed into `NSArray` and `NSDictionary` literals, as this will cause a crash.

**For example:**

```objc
NSArray *names = @[@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul"];
NSDictionary *productManagers = @{@"iPhone": @"Kate", @"iPad": @"Kamal", @"Mobile Web": @"Bill"};
NSNumber *shouldUseLiterals = @YES;
NSNumber *buildingZIPCode = @10018;
```

**Not:**

```objc
NSArray *names = [NSArray arrayWithObjects:@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul", nil];
NSDictionary *productManagers = [NSDictionary dictionaryWithObjectsAndKeys: @"Kate", @"iPhone", @"Kamal", @"iPad", @"Bill", @"Mobile Web", nil];
NSNumber *shouldUseLiterals = [NSNumber numberWithBool:YES];
NSNumber *buildingZIPCode = [NSNumber numberWithInteger:10018];
```

## CGRect Functions

When accessing the `x`, `y`, `width`, or `height` of a `CGRect`, always use the [`CGGeometry` functions](http://developer.apple.com/library/ios/#documentation/graphicsimaging/reference/CGGeometry/Reference/reference.html) instead of direct struct member access. From Apple's `CGGeometry` reference:

> All functions described in this reference that take CGRect data structures as inputs implicitly standardize those rectangles before calculating their results. For this reason, your applications should avoid directly reading and writing the data stored in the CGRect data structure. Instead, use the functions described here to manipulate rectangles and to retrieve their characteristics.

**For example:**

```objc
CGRect frame = self.view.frame;

CGFloat x = CGRectGetMinX(frame);
CGFloat y = CGRectGetMinY(frame);
CGFloat width = CGRectGetWidth(frame);
CGFloat height = CGRectGetHeight(frame);
```

**Not:**

```objc
CGRect frame = self.view.frame;

CGFloat x = frame.origin.x;
CGFloat y = frame.origin.y;
CGFloat width = frame.size.width;
CGFloat height = frame.size.height;
```

## Constants

Constants are preferred over in-line string literals or numbers, as they allow for easy reproduction of commonly used variables and can be quickly changed without the need for find and replace. Constants should be declared as `static` constants and not `#define`s unless explicitly being used as a macro.

**For example:**

```objc
static NSString *const SMEAboutViewControllerCompanyName = @"1kLabs, Inc.";

static const CGFloat SMEImageThumbnailHeight = 50.0;
```

**Not:**

```objc
#define CompanyName @"1kLabs, Inc."

#define thumbnailHeight 2
```

## Enumerated Types

When using `enum`s, it is recommended to use the new fixed underlying type specification because it has stronger type checking and code completion. 
The SDK now includes a macro to facilitate and encourage use of fixed underlying types — `NS_ENUM()`

`enum` names should be prefixed with the base name followed by the specific name.

**Example:**

```objc
typedef NS_ENUM(NSInteger, SMEPhotoType){
    SMEPhotoTypeWho,
    SMEPhotoTypeWhat,
    SMEPhotoTypeWhere
};
```

## Private Properties

Private properties should be declared in class extensions (anonymous categories) in the implementation file of a class. 
Named categories (such as `SMEPrivate` or `private`) should never be used unless extending another class.

**For example:**

```objc
@interface SMEPhoto()

@property (strong, nonatomic) SMEUser *user;
@property (nonatomic) SMEPhotoType photoType;
@property (nonatomic) NSInteger guessCount;

@end
```

## Image Naming

Image names should be named consistently to preserve organization and developer sanity. 
They should be named as one pascal-case string with a description of their purpose, 
followed by the un-prefixed name of the class or property they are customizing (if there is one), 
followed by a further description of color and/or placement, and finally their state.

**For example:**

* `RefreshBarButtonItem` / `RefreshBarButtonItem@2x` and `RefreshBarButtonItemSelected` / `RefreshBarButtonItemSelected@2x`
* `ArticleNavigationBarWhite` / `ArticleNavigationBarWhite@2x` and `ArticleNavigationBarBlackSelected` / `ArticleNavigationBarBlackSelected@2x`.

## Booleans

Since `nil` resolves to `NO` it is unnecessary to compare it in conditions. Never compare something directly to `YES`, because `YES` is defined to 1 and a `BOOL` can be up to 8 bits.

This allows for more consistency across files and greater visual clarity.

**For example:**

```objc
if(!someObject){
}
```

**Not:**

```objc
if(someObject == nil){
}
```

-----

**For a `BOOL`, here are two examples:**

```objc
if(isAwesome)
if(![someObject boolValue])
```

**Not:**

```objc
if([someObject boolValue] == NO)
if(isAwesome == YES) // Never do this.
```

-----

Deriving truth value directly from an arithmetic operation is never a good idea. 
Instead, use the result of the == operator, or cast values into booleans with the ! (or !!) operator.

**For example:**

```objc
NSInteger age = 12;
if(!!age){
    // age is not 0
}
```

or

```objc
NSInteger age = 12;
if(age != 0){
    // age is not 0
}
```

From [NSHipster BOOL](http://nshipster.com/bool) post.

-----

If the name of a `BOOL` property is expressed as an adjective, the property can omit the “is” prefix but specifies the conventional name for the get accessor, for example:

```objc
@property (getter=isEditable) BOOL editable;
```
Text and example taken from the [Cocoa Naming Guidelines](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/Articles/NamingIvarsAndTypes.html#//apple_ref/doc/uid/20001284-BAJGIIJE).

## Singletons

Singleton objects should use a thread-safe pattern for creating their shared instance.

```objc
+ (instancetype)sharedInstance{
   static id sharedInstance = nil;
   static dispatch_once_t onceToken;
   dispatch_once(&onceToken, ^{
      sharedInstance = [[self alloc] init];
   });
   return sharedInstance;
}
```

This will prevent [possible and sometimes prolific crashes](http://cocoasamurai.blogspot.com/2011/04/singletons-your-doing-them-wrong.html).

# References

Many of the Objective-C guides are from the [New York Times: Objective-C Style Guide](https://github.com/NYTimes/objective-c-style-guide), much of the text is stright up copied because they did such a great job with it!
