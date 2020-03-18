## Basic Branch/Pull Request information
If you followed the Server set-up instructions, you've already cloned topaz's master branch (called release). If you want to make changes and contribute to Topaz, here's a quick guide on how to push changes.

1 - Set up your fork on github if you haven't already. this is where you'll push changes to then submit a pull request. You can click on the fork button above the main project-topaz/topaz repository to fork. 

2 - Set up a .gitignore file. If you're running an era server, your version info will always be set to 0 vs. the default 1. If you don't add versioninfo to git ignore, it will try to commit it and add to every pr you do.

3 - Make a new branch for any changes. Do NOT make your changes on master unless you don't plan on making a pull request to contribute. Making changes on master will prevent you from making changes elsewhere until the PR is reviewed and incorporated. You can make a branch for anything, but typically it's for a unit of work (which could be something as overarching as sql edits for all mobs or something more project focused like a single bcnm)

Right click on your topaz install and choose "make branch". Create the name of the branch and then right click on your topaz install and choose switch and checkout to change to the branch. If you've made any changes at this point, you'll get an error and be forced to commit or stash your changes. Commit means actually resolving the changes with your local and master branch, a true save. Stash is a temp save. 

4 - In the new checked out branch, make the changes as needed. When you've tested and are comfortable with the work, right click on your topaz install folder and choose to commit the branch. In the window that appears, make sure any changes that aren't inline with topaz master (for instance, I have my version info file changed so i can use an older version, but I would not want to commit that) are not included in your commit. You can choose commit and push here to then send the changes to your remote repository from your local. 

5 - In your remote repository, make sure you're on your branch that you're looking to contribute from and select New pull request. Fill out the relevant checkboxes, put in an appropriate title, etc.

6 - Upon review and completion your pull will be merged with topaz's release branch, or the canary branch if it's a large enough or changed enough feature to warrant testing before final merge into release. 

NOTE: for custom servers, it's probably best to have a separate repository entirely for custom data vs. topaz's build. That way you can clone/download/change/commit for any fixes direct to a separate repository and install. 

## Keeping current with Topaz
You'll want to consistently update your master with recent changes submitted by contributors, that's part of why working on branches when you have WIPs is important. In order to update both your local and remote master:
1) Ensure you're on your master branch and have no other local branches checked out
2) Choose "Pull" from the menu of whichever Git tool you're using
3) Select the topaz remote branch to merge. Remember Topaz's master branch is called "release". If you haven't pulled from Topaz in a while, you'll want to do a "Fetch" first to update the remote listings in your Git tool.
4) Pull from release into your master. 
5) You'll now need to update your remote repository to reflect using the "Push" command. Merge your master with your remote origin


## Submitting to multiple repositories
[You can use git rebase](https://github.com/edx/edx-platform/wiki/How-to-Rebase-a-Pull-Request) to send commits from other locations to topaz in order to submit to multiple locations and/or repoint.

Alternatively, pull a fork of topaz and copy **changes only** manually. 




