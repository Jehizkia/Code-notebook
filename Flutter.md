# Flutter snippets


# stateless widget shortcut
Type in android studio:
```
stless
```
And press enter to insert boilerplate code for a stateless widget.



# Auto completion import issues
If you have issues with the auto complete of import packages you can try to delete these folders and files.
```
.dart_tool
.packages
.pubspec.lock
```
When deleted you'll need to run ``` pub get ``` to generate all the files and folders again.
Source: https://github.com/flutter/flutter-intellij/issues/4229
