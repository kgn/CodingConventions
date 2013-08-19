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
