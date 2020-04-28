# Personal website [![Netlify Status](https://api.netlify.com/api/v1/badges/bd9b2588-be1d-4bb3-b2fa-fec3cd8e5ae0/deploy-status)](https://app.netlify.com/sites/theredthread/deploys)

## Intro
...
## Workflow

Create the hugo site as follows:
```bash
$> hugo new site <website name>
$> cd <website name>
$> git init
$> git submodule add https://github.com/alex-shpak/hugo-book themes/book
$> git submodule add https://github.com/luizdepra/hugo-coder.git themes/hugo-coder
$> git add --all
$> git status # a bunch of files will be ready to commit now
$> git commit -m "Starting website and adding two themes" # Git purists will split this in three commits
```
Create a fresh repository in github, add it as remote and push from the client:
```bash
$> git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
$> git push -u origin master
```

Updating the website contents
...


## Resources
...

