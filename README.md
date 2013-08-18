Main items like repo names, folders, and classes are in [Pascal Case](http://c2.com/cgi/wiki?PascalCase).

Lesser items like class properties and variables are in [Camel Case](http://msdn.microsoft.com/en-us/library/x2dbyw72.aspx).

The Sesame namespace is `SME`. This should be used for all Cocoa, Pytnon, and JavaScript/CoffeeScript global objects.

# Git Repos

Get repositories are Pascal Case and name-spaced with *Sesame*. 

Examples *SesameCocoa*, *SesameWebsite*.

# Get Branches

Github branches are Pascal Case and use `/` so that branches are organized into *directories* in GUI apps.

Namespaces:
- Feature - A feature branch. Examples: `Feature/SoundControl`, `Feature/XRay`
- Build - A build branch for the build system. Examples: `Build/Release`, `Build/Beta`.
