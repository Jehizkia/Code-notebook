# General 


### Tracking down broken functionality or code
Sometimes you'll get a very vague error or no error at all. The code doesn't work and you want to find out where exactly it goes wrong.
I will give you an example how I tackle this problem with phpstorm.

Make create new branch from your dev or master branch. Any branch is fine, just make sure your application is in a working state.

1. Checkout into the newly created branch.
2. In phpstorm go your branch overview.
3. Select the branch which contains the broken code
4. Select: Show Diff with working Tree
5. Phpstorm will show you on the left you new branch and on the right the branch with your broken code
6. Using the arrows you can import pieces of your code into the current branch.
7. Make sure you import the pieces of code that let your application run without problems (ex. imports).
8. And now slowy the other pieces of code and re-run/refresh page to test if the application breaks
9. If you have found the culprit you can fix the problem in your original branch or keep working in the newly created.

This explanation might be vague but if you come across this small and unkown repo and have questions you can always contact me.
