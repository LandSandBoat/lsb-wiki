If you plan to run your own server using the Topaz codebase, you'll want your own copy of the code repository. The best way to achieve this is to **fork**.

### Creating your fork

GitHub provides an easy to use button in the top right of the front page of any repo, allowing you to create a full copy of the repo from that point in time. This copy will include all of the commit history and changes up to that point. This is important because your fork will have a **shared history** with the Topaz codebase. This will allow you to easily cherry-pick code, or pull in feature branches from Topaz. 

### Git Pull

### Cherry-Picking
Cherry-picking is an operation available through git, allowing you to take a full commit; including the original git revision hash and author information. Copy/pasting will not preserve this information and create situations where you are unable to easily take new changes from upstream because you have conflicts between your copy/pasted code and the original work. Erasing the original author information is also a violation of the Topaz License.

### Defensive Design
If you plan on making heavy modifications to the Topaz codebase while still recieving changes from it, you will likely want to employ some *defensive design* techniques to make sure your changes are not overwritten by the incoming Topaz changes.

- **Keep changes in separate files.** If you replace a function call with your own that you keep in it's own file, you will have less possible sources of collision. If you keep your SQL changes in a file that is applied after the regular Topaz update, you never have to resolve conflicts.

- **Block comments.** If you employ `/* block */, --[[ block ]]` comment style around large blocks you are commenting out, you will only have to resolve changes on two lines, rather than the entire block in question.

- **Mark your custom changes so they are easy to spot.** Marking a block with `// Custom server X's stat calculations` will make sure it's very easy to spot and maintain when you're resolving conflicts.

- **Namespacing.** If you're replacing logic in specific function calls, you could keep your custom work in a namespace. `NewServer::GetRandomNumber()` is very clearly specific to your server.

### Understanding the Topaz License



