## What are Git and GitHub?
1. git is a version control system for tracking and saving changes in your code
2. github is a website for hosting your git repositories (projects)

## How to use?
### step1 create a new repository in github
![[Pasted image 20250818160324.png]]
### step2 push to github with git after code (local) over
#### push in the first time
*  initialize the repository
	* `git init`
* add files to temp area
	* `git add .` (can write detail file like git add style.css, and if only . stands for all)
* commit to local repository
	* `git commit -m ""` (write descripe in " ")
* change the branch name
	* `git branch -M main`
* collect the remote resository in github
	* `git remote add origin https://github.com/Potterprogramme/git-and-github-tutorial.git
* push local to github
	* `git push -u origin main
#### after code change
* add files to temp area
	* `git add .`
* commit to local repository
	* `git commit -m "description"`
* push to github
	* `git push`
