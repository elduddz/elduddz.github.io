# scratch
# working title : Guide to being Git...ish 

## Creator 

Git was created by Linus Torvalds (Linux) 

## What is Git
- Invented by Linus Torvalds  
- Distributed Revision Control System  
- Allows a working model, that allows developers to be both a node and hub.  
- Everyone has the full repository with them. The control and repository in that way is distributed amongst it users.  

## Porcelain commands

- add [.] -f (-f  allows you to add files you might normally ignore, such as dlls)
- commit [-m] 
- push 
- pull 
- branch 
- checkout 
- merge 
- init 
- status
- log 
- gui 
- k 

## Plumbing commands 
- cat-file 
- hash-object 
- count-objects

Usually spend most of time in porcelain commands 

## Break down of Git 

- “A Distributed Revision Control System” 
- Remove distribution, it becomes a Revision Control System 
- Remove history, branches and merges, it becomes a Stupid Content Tracker 
- Remove commit or versioning, it becomes a persistent Map. 

## What does does it mean when you say git is a map 

- a table of keys and values 
- values are a sequence of bytes 
- given a sequence of bytes git will generate a SHA1 (shaone) 
- this becomes gits key to store the content 
- every object in git has it's own SHA1 
- has a high probability of never colliding 

## Getting started 

git init - creates .git

## looking in .git 
start .git 

after adding some objects check .git/objects directory starts with first 2 characters of SHA1 made up of 3 types 

**Git Object Model**

- Blob - this is just the content of file, the file name and file permissions are stored in the tree.  
- Tree - list of the content of the directory, a list of SHA1  
- Commits (each commit)
- Annotated Tags  

using git cat-file -p [SHA1] allows you to see the content of the SHA1

looking at the logs you can find the SHA1 of the commits, each subsequent commit will have a linked parent(s).

Git will reused objects in different commits if nothing has changed.

Git will start a new blob every time you change a file, but there is a layer of optimisation, as you keep working on adding content, git might choose to only save the differences. but is easier to think of each object as being related to a unique SHA1.

## git cat-file 

git cat-file -p sha1 

-p pretty   
-t type  

using git hash-object will create a hashed object for the content submitted.  

## .gitignore
To help with exculsions of files that you might not want, you can add a repo level .gitignore file.

example: at root of repo, if I create a file called .gitignore (vi .gitignore) and add the following  
obj/   
bin/  
.suo  

any files below the area of obj and bin will be ignored as will any file of type .suo

_Visual Studio has a default .gitignore that covers most of the expected objects_

## Tag

- **(lightweight) Tag**  
  - git tag tagName  
- **annoted Tag**   
  - get tag -a mytag -m "I love git"  

Tags are a pointer to a SHA1, so you can cat-file the tag or the SHA1.

## What is Git

We thing that contain data called blobs, then things called trees that contains blobs and trees, the names of the blobs are named in the same tree.
 
This means you can have the same blob with different names in 2 different trees.
 
Version File System. Git is a content tracker (Stupid Content Tracker)

## Merge vs Rebase
- Merges preserve history  
  - A merge never lies, it is always a unique entry  
- Rebasing refactories history
  - A rebase history looks cleaner but changes project history  
- when in doubt merge   

## Headless
git checkout [sha1]

## Distributed working  
- git clone  
- git fetch

## moving about the source
- git reset [--hard|--soft]  

## sources: 

- https://git-scm.com/ 
- https://app.pluralsight.com/library/courses/how-git-works 
- Paulo Perrotta [@Nusco](https://twitter.com/nusco)
