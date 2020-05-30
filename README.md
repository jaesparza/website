# Personal website [![Netlify Status](https://api.netlify.com/api/v1/badges/bd9b2588-be1d-4bb3-b2fa-fec3cd8e5ae0/deploy-status)](https://app.netlify.com/sites/theredthread/deploys)

## Intro
In this project I am trying out Hugo, a static web generator. Some of the advantages if compared to traditional CMS:
* Little-to-no server maintenance (no php or SQL server)
* Sensible deployment workflow via Netlify
* Free hosting on GitHub

Aditionally, no cookies get created and one has more control on what information is collected (easier GDPR compliance).

## Workflow
### Installation
Install via binaries https://github.com/gohugoio/hugo/releases
Avoid installing via package repo (apt-get ...) since these repositories have been many releases behind the latest one. This causes some features and themes to be incopatible.

Get good tools: a git client (gitkraken or sublime-merge), and VScode for text editing.

### Creating the basic website and adding a theme
Get a terminal and start by creating the basic skelenton and themes ready for the commit:
```bash
$> hugo new site <website name>
$> cd <website name>
$> git init
$> git submodule add https://github.com/alex-shpak/hugo-book.git themes/book
$> git submodule add https://github.com/luizdepra/hugo-coder.git themes/hugo-coder
$> git add --all
$> git status # a bunch of files will be ready to commit now
$> git commit -m "Starting website and adding two themes" # Git purists will split this in three commits
```
The folders content, data, layouts and static are empty after creation therefore will not be commited to git. To force git to place them under version control, creat an empty ".gitignore" file in each folder, and repeated git add and commit steps.


In order to publish in github, create a fresh repository in github, add it as remote and push from the client:
```bash
$> git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
$> git push -u origin master
```

### Updating the website contents:
Edit locally. e.g. - let's create a new post:
```bash
$> hugo new posts/my-first-post.md
```

Preview changes by launching the server:
```bash
$> hugo server -D --minify --theme hugo-coder # here we force the theme hugo-coder to be used
```
Go to a web-browser and launch http://127.0.0.1:1313/

If you are satisfied with the results:
```bash
$> git add --all # Here add all all changes for commit or alternatively select the relevant ones
$> git commit -m "your message"
$> git push -u origin master
```

### Notes on submodules for themes

When cloning, remember to initialize the submodules for the themes. From the root of the repository:
```
$> git submodule update --init
```

Updating the submodule:
```
$> git pull origin master
$> cd ..
$> git add (NAME) # Name of the submodule here
$> git commit -m "Submodule updated"
$> git push
```
or

```
$> git submodule update --remote --merge
```

### Working with branches

Netlify under my configuration will deploy off master branch. To work on drafts I make branches that can be later merged into master for deployment.

Create the new branch and push it to remote:
```
$> git pull
$> git checkout -b (NAME) ## name of new branch
$> git push origin (NAME) ## name of new branch
$> git branch -a # this will show the new branch both locally and in remote
```

Switch to branch (NAME), this can be master or a different one:
```
$> git checkout master ## switch branch to master
```

To peform local changes in the new branch and submitted to the remote one, first registere it:
```
$> git push --set-upstream origin (NAME)
$> git push ## will send changes to remote (NAME)
```

To merge changes from master into the branch (NAME), assuming that (NAME has ben checkedout)
```
$> git rebase master
$> git push ## changes will be sent upstream
```
To list all the branches in the repository
```
$> git branch -a
```

## Resources
* Markdown format cheatsheet https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet
* Hugo book theme https://themes.gohugo.io/hugo-book/
* Hugo coder theme https://themes.gohugo.io/hugo-coder/
* Create a website for 12$ - Step by step tutorial - [Youtube Playlist](https://www.youtube.com/playlist?list=PL-Kz5P-mYdMgAJDmRJquyMHfdaIOD-3oj)
* Hugo quick start https://gohugo.io/getting-started/quick-start/ 
