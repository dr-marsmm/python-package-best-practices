title: "Intro to Version Control with Git"
- "How do I use git to keep a record of my project?"
- "Understand how to view and check out previous versions of files."
- "Git provides a way to track changes in your project."
- "Git is a software for version control, and is separate from GitHub."
facilitates collaboration on projects where everyone can work freely on a part
versions and rollback when needed. Also, you can review the
history of your project through commit messages that describe changes on the source code
and see what exactly has been modified in any given commit. You can see who made the
You should have git installed and configured from the [setup] instructions.

In this section, we are going to  edit files in the Python package that we created earlier, and use `git` to track those changes.
$ ls -la
{: .bash}
This tells us that we are on the `master` branch, and that no files have been changed since the last commit.
## The 3 steps of a commit

Now, we will change some files and use `git` to track those changes. Let's edit our README. Open `README.md` in your text editor of choice. On line 8, you should see the description of the repository we typed when running the CookieCutter. Add the following sentence to your `README` under the initial description.
#### git add, git status, git commit
Making a commit is like making a checkpoint for a particular version of your code. You can easily return to, or revert to that checkpoint.

To create the checkpoint, we first have to make changes to our project. We might modify *many* files at a time in a repository. Thus, the first step in creating a checkpoint (or commit) is to tell `git` which files we want to include in the checkpoint. We do this with a command called `git add`. This adds files to what is called the *staging area*.
Let's look at our output from `git status` again.
        modified:   README.md
Git even tells us to use `git add` to include what will be committed. Let's follow the instructions and tell `git` that we want to create a checkpoint with the current version of `README.md`
        modified:   README.md
We are now on the second step of creating a commit. We have `added` our files to the staging area. In our case, we only have one file in the staging area, but we could add more if we needed.
To create the checkpoint, or commit, we will now use the `git commit` command. We add a `-m` after the command for "message." Whenever you create a commit, you should write a message about what the commit does.
$ git commit -m "update readme to have instructions for developmental install"
Now when we look at our log using `git log`, we see the commit we just made along with information about the author and the date of the commit.
Let's continue to edit this readme to include more information. This is a file which will describe what is in this directory. Open `README.md` in your text editor of choice and add the following to the end 
This package requires the following:
  - numpy
  - matplotlib
This file is using a language called [markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet). 
> ## Check your understanding
> Create a commit for these changes to your repository.
>> ## Answer
>> To add the file to the staging area and tell `git` we would like to track the changes to the file, we first use the `git add` command.
>> ~~~
>> $ git add README.md
>> ~~~
>> {: .language-bash}
>> Now the file is *staged* for a commit.
>> Next, create the commit using the `git commit` command.
>> ~~~
>> $ git commit -m "add information about dependencies to readme"
>> ~~~
>> {: .language-bash}
> {: .solution}
{: .challenge}
Once you have saved this file, type
$ git log
{: .language-bash}
Now, check `git status` and `git log`. You should see the following:
nothing to commit, working tree clean
$ git log
We now have a log with three commits. This means there are three versions of the repository we are working in.
`git log` lists all commits  made to a repository in reverse chronological order.
The listing for each commit includes the commit's full identifier,the commit's author, when it was created, and the commit title.
We can see differences in files between commits using git diff.
$ git diff HEAD~1
{: .language-bash}
Here HEAD refers to the point in our commit history (and current branch). When we use `~1`, we are asking git to show us the different of the current point minus one commit.
Lines that have been added are indicated in green with a plus sign next to them ('+'), while lines that have been deleted are indicated in red with a minus sign next to them ('-')
## Viewing out previous versions
If you need to check out a previous version
$ git checkout COMMIT_ID
This will temporarily revert the repository to whatever the state was at the specified commit ID.
Let's checkout the version before we made the most recent edit to the README.
$ git log --oneline
d857c74 (HEAD -> master) add information about dependencies to readme
3c0e1c6 update readme to have instructions for developmental install
116f0cf (tag: 0.0.0) Initial commit after CMS Cookiecutter creation, version 1.1
In this log, the commit ID is the first number on the left.
To revert to the version of the repository where we first edited the readme, use the git checkout command with the appropriate commit id.
$ git checkout 3c0e1c6
{: .language-bash}
If you now view your readme, it is the previous version of the file.
To return to the most recent point,
$ git checkout master
> ## Exercise
> What list of commands would mimic what CMS CookieCutter did when it created the repository and performed the first commit? (hint - to initialize a repository, you use `git init`)
> > ## Solution
>> To recreate the CMS Cookiecutter's first commit exactly,
>>~~~
$ git init
$ git commit -m "Initial commit after CMS Cookiecutter creation, version 1.0"
>>~~~
>>{: .language-bash}
>>  
>>  
>>The first line initializes the `git` repository. The second line add all modified files in the current working directory, and the third line commits these files and writes the commit message.
> {: .solution}
{: .challenge}