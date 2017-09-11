## Setting the scene  

I think we have all be there, perform a commit, then realised it has a file that contains a password or some other identifying information that could be a security breach. If that is the previous commit you are fine, still havent pushed to your remote things are OK, already pushed to the remote, you still have a few options.

That being said, you cannot really rewrite history, but I say you can... sort of...

Let's investigate the options.

As the title suggests, the version control we are looking at is git, so let's start from the top.

## What is git?  

You will find more details provided by experts, but the basics are git is a version control system, more specifically it is a distributed version control system. How this differs from others like subversion and TFVC, is that each person holds a version of the source that is then able to be shared with a central repository via various provisions (github, etc) and also directly with each other. An example of this was, for some odd reason, I was able to connect with guthub, but a colleague couldn't, so I acted as a relay by provided a version of the source from my machine that they could then work against and I would then sync up for them.

In a similar vein to other version control systems, you can see a historical record about your repository.

Git-scm comes with tools like gitk to help with visualisation of the history and git gui to help with committing. GitHub and Atlassian have created products that work with git, but they are basically abstracting away the function that is going on on the command line.

I would also advise installing some compassion software, beyond compare is good, but comes with a price tag. For a free option I would suggest installing tortoisesvn as that comes with tortoisemerge, rinse you will be defaulting to vi.

Using these visualisation tools, you can look at any point in time on your repository you hope to fix.

What you will see are all the committee you have made, and against each is a key which is an Sha1, using this you can access any point in your history.

```bash
git reset --soft sha1

git commit -m "shhhh, they'll never know"
```