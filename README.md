# Learn Git
The purpose of this repository is to teach the basics of Git. Learn a little bit about git and why we use it @ [The Git Parable](http://tom.preston-werner.com/2009/05/19/the-git-parable.html). The core of our branching model comes from [The Gitflow](https://datasift.github.io/gitflow/IntroducingGitFlow.html)

Please read [important warnings and best practices](#important-warnings-and-best-practices).

We'll cover:
- [Installing Git](#install-git)
- [Cloning your project](#clone-your-project)
- [Pulling the latest code](#pull-the-latest-code)
- [Creating a new branch](#create-a-new-branch)
- [Checking the branch status](#checking-the-branch-status)
- [Commiting/saving your work](#commit-saving-your-work)
- [Reverting mistakes](#reverting-mistakes)
- [My branch has changes that are not mine, help!](#fixing-bad-branches)
- [Important warnings and best practices](#important-warnings-and-best-practices)

To demonstrate your knowledge, we'll do [simple lab](#demonstrate-your-skills).


### Install Git
Git is available on a variety of platforms. Just follow the [install instructions](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).

### Clone your project
Get a copy of project code. You'll only need to do this once per computer/server you plan to do your coding on:
- Go to the Github page for the project
- Click "Clone or download" on the righthand side of the page
- Copy the URL
- Run: `git clone <PROJECT URL WE COPIED>`

### Pull the latest code
Refresh your copy of `production` code (`production` is a branch in this case, more on that in a second):
```
git checkout production
git pull origin production
git merge --abort
git reset --hard origin/production
```

### Create a new branch
#### What's a branch and why do I need it
Think of the multiverse concept you have seen in movies. There are parallel universes, each with slightly different realities. For example, maybe Bob is married to Jane in Universe A but Bob is married to Mary in Universe B.
Git is similar. We take the production code branch (Universe A), and make an exact copy of it (Universe B). We then can make changes to the copy without affecting the code for everybody else.

#### Commands to create new branch
All branches should be associated with a ticket (see warnings section)
```
git checkout -b branch-name-based-on-ticket-####
```

Then you're good to start making changes!

### Checking the branch status
At any point, you can list what changes you have made by running:
```
git status
```
Files in red have not been saved yet. Files in green have been `git add`, but not fully saved/committed (see below)

### Commit (saving your work)
After making some changes, start a "commit".

Typically you want to add all changes you have made:
```
git add --all .
```
The `--all` signals that you want to add new files that didn't exist before. The `.` signals that you want to add all files with changes.

If you only want to add specific files, run:
```
git add <LIST OF FILES>
```

Then commit (save) them:
```
git commit -m "<brief description of your changes>"
```
This saves them to your LOCAL environment. To push the code to Github (we wouldn't want to lose code if you lose your laptop or your server crashes!):
```
git push origin branch-name-based-on-ticket-####
```

Post a pull request in Gitub to let others give feedback and look for bugs (this is mandatory if you want your code to be published):
- Go to the Github project page
- On the lefthand side there is a dropdown box labeled `Branch: <some branch`. Click it and select your branch
- Click "New pull request"
- Enter details about your changes
- Add a `code-review` label
- Click "Create pull request"

### Reverting mistakes
Often you'll need to revert an entire file of changes back to what it was previously. If the file hasn't been committed yet:
```
git checkout <path to file>
```

If the file has been added (ie. `git add`):
```
git reset <path to file>
git checkout <path to file>
```

### Fixing bad branches
Accidents happen and sometimes you'll forget to [start off on the production branch when making new features](#pull-the-latest-code). You end up with a bunch of files in your change that you didn't actually change. Essentially you started with a bunch of changes and built your feature on top of that. It's a problem because not all of the changes in the branch you started from were valid (ie. more changes were made, some changes made it to production, some changes were probably removed entirely, etc). That's why following the [new branch guide](#pull-the-latest-code) for *every single new branch* is really important.

To fix the problem, there's two options to handle this:
- Recreate changes from scratch in a new branch by selecting only the changes that are valid from the old branch
- Removing the changes that are invalid from the branch (basically do this instead of the above if the number of bad files < number of valid files)

As an example let's step through the first method by creating a new branch. You're going to have to go through each file in the bad branch and determine if it has changes in it that you made or not. If the file *DOES* have changes, then we'll move that file over to the new branch.
- Follow steps for [creating a new branch](#pull-the-latest-code)
- For every file in the PR that is valid and has your changes, run `git reset <REPLACE WITH OLD BRANCH NAME> <REPLACE WITH FILENAME>`. For example, if the `Gemfile` has changes and your bad branch is named `my-bad-branch-1234`, you'd run `git reset my-bad-branch-1234 Gemfile`
- Once you've gone through all the files and are confident you have selected which ones are valid (ie. doing the above), run `git checkout .`
- If any files had changes that you made AND had changes that you didn't make, you need to go and manually edit the files to replace the lines of code that you didn't change
- Add all changes: `git add .`
- Commit the changes: `git commit -m "<REPLACE WITH YOUR MESSAGE>"`
- Push the new branch with the correct files to github: `git push origin <REPLACE WITH YOUR CURRENT BRANCH NAME>`
- Create a new PR and close the old, invalid PRs

## Important warnings and best practices
- You should typically only ever need a few Git commands, such as creating a new branch and pushing to Github
- If you are force merging anything - you're probably doing something wrong. **Ask**.
- Rebasing/merging is difficult at times - if you are unsure about any of it, **Ask**.
- All your branches should co-relate to a ticket. Otherwise others won't be able to see what you're doing and work alongside you. If you have an idea and want to work on it, just create a simple ticket first. Ideally go with the team priorities as laid out in [Active Work](https://github.com/orgs/BustrInc/projects/2).
- Along with the note above, all branches for tracking should end in a ticket number. For example, if there is a ticket with issue number "3873" you'd name the branch "your-change-name-3873". Publishing scripts and humans can match any branch by this number to the issue it belongs.


## Demonstrate your skills
To demonstrate your knowledge of Git, try to complete the following lab:
- Clone [this project](https://github.com/BustrInc/LearnGit)
- Create a new branch from production
- Create a new empty text file to the root of this project with your email as the filename:
  - For example, I would create a file "bengineer.txt" since my email is "bengineer@buster.com"
- Add the new file to a commit
- Ask someone to add you as a collaborator to this project (or the next steps will fail)
- Push your branch to Github
- Create a code review
