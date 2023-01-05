# Git Note
## _QuickStart_
### First time push to remote repo(GitHub)
```commandline
touch .gitignore 
git init
git add -A
git status
git commit -m 'message'
git branch -M main
git remote add origin https://github.com/rolny/git.git
git push -u origin main
```

## Setting user info
Every **Repository** has own config
We should set parameter in config

### git config
```commandline
git config --global user.name <argument>
```
<dl>
<dt><a>--list</a></dt>
<dd>enumerate current configuration</dd>
<dt><a>user.name</a></dt>
<dd>setting user name</dd>
<dt><a>user.email</a></dt>
<dd>setting user email</dd>
<dt><a>--global</a></dt>
<dd><code>--global</code> used to setting all repository configuration. Do not add this parameter if you don't want config all</dd>
</dl>

> You can set the name same as [_**GitHub Account**_](https://github.com/) 

## Startting Git (Local) 
### Initialization
Initialize folder, it will add a hidden folder ".git"
```commandline
git init
```
### Check Status
Check commit and tracking status
```commandline
git status
```
### Track File
To include in what will be committed, it will move to **_Staging Area_**
```commandline
git add <file>
```
>add file in current directory `git add .`, add all file and directory `git add -a `
### Changes to be committed
To unstage, move file in **_Staging Area_** to **_working directory_**
```commandline
git rm --cached <file>
```
### Changes to be committed
To unstage, move file in **_Staging Area_** to **_localrepo_**, 
and edit message with **vim**
```commandline
git commit
```
However, we can type `-m` for message with one sentence
```commandline
git commit -m <message>
```
If in a situation, we add files one after another rather than in same time,
we can use `--amend`, to merge all commit to this commit
```commandline
git commit --amend -m <message>
```
### Check commit log
We will get the log,which is top to bottom from new to old
```commandline
git log <version>
```
<dl>
<dt><a>--oneline</a></dt>
<dd>a concise output</dd>
<dt><a> file </a></dt>
<dd></dd>
<dt><a>-p</a></dt>
<dd>increase verbosity level</dd>
<dt><a>--author</a></dt>
<dd><code>git log --author="name"</code>check specific author's commit</dd>
<dt><a>--grep</a></dt>
<dd><code>git log --grep="string"</code>check specific string</dd>
<dt><a>--since, until</a></dt>
<dd><code>git log --since="9am" --until="17pm"</code>check period of time</dd>
</dl>

## git common script
### git rm
Use git to remove file
```commandline
git rm <filename>
```
### git mv
Use git to rename file 
```commandline
git mv <originFileName> <newFileName>
```
### git checkout
Switch version/branch
```commandline
git checkout <version/brach>
```
- _tips_
  1. Switch to last version`git checkout master`
  2. Cancel modify in _**Staging Area**_ `git checkout --`
  3. Restore file `git checkout <FileName>`
### git diff
Compare the file between two area
 - _**e.g.**_
   1. Compare the file between _**Working Directory**_
      and _**Staging Area**_ `git diff --cached`
   2. Compare current file with the file in _**Staging Area**_
      `git diff <FileName>`
   3. Compare specific commit with _**Working Directory**_
      `git diff <commit-id>`
   4. Compare different between two commit/branch `git diff <commit-id/branch1> <new commit-id/branch2>` 
### git reset
Go to the last commit
<dl>
<h3>reset mode</h3>
<dt><a>--mixed</a></dt>
<dd>Default parameter.reset <i><b>Staging Area</b></i> but do not affect <i><b>Working Directory</b></i></dd>
<dt><a>--soft</a></dt>
<dd>In this mode, <i><b>Staging Area</b></i> and <i><b>Working Directory</b></i> files were keep, only move <b>'HEAD'</b></dd>
<dt><a>--hard</a></dt>
<dd>In this mode, <i><b>Staging Area</b></i> and <i><b>Working Directory</b></i> files were abandon</dd>
</dl>

| Mode                      | Mixed                           | Soft                       | Hard          |
|---------------------------|---------------------------------|----------------------------|---------------|
| _**Working Directory**_   | unchanged                       | unchanged                  | abandoned     |
| _**Staging Area**_        | abandoned                       | unchanged                  | abandoned     |
| reset files               | move to _**Working Directory**_ | move to _**Staging Area**_ | abandoned all |

### git ignore
Some file in repository wouldn't track by git, we can create a .gitignore file, then add filename/directory/file extension

Edit .gitnore 
```commandline
node_modules
packages/react-devtools-core/dist
*.crx
```
## Git remote operation script
### git remote
Use `git remote` we can check all remote repo **short**
```commandline
$ git remote
origin
```
add `-v` can show url of remote repo
```commandline
$ git remote -v
origin  https://github.com/rolny/git_note.git (fetch)
origin  https://github.com/rolny/git_note.git (push)
```
Add remote repo to local repo use `add`
```commandline
git remote add <remote repo short> <url>
```
### Download git from remote
- _**git clone**_
  
  Clone entire git repository
  ```commandline
  git clone <url>
  ```
  Clone with other name
  ```commandline
  git clone <url> <local repo name>
  ```
- _**git fetch**_
  
  Download branch from remote repository
  ```commandline
  git fetch <remote repo short> <remote branch>
  ```
  - Fetch didn't combine local repo and remo repo, therefore after done `git fetch`
    we need use `git merge` for merge both branch
  
  #### Two ways for use git fetch to update local repo
  #### 1. 
  ```commandline
  git fetch origin master              #download branch
  git log -p master.. origin/master    #compare diffrent between two repo
  git merge origin/master              #merge 
  ```
  #### 2.
  ```commandline 
  git fetch origin master:temp        #downlaod branch master of repo origin and crete
  git diff temp                       #compare diffrent between two repo
  git merge temp                      #merge branch temp to branch master
  git branch -d temp                   #delete temp
  ```
- _**git pull**_
  
  Download remote repo to local repo. Basically, _git pull_ equivalent to fetch 
  the latest version from remote repo, then merge local branch
- ```commandline
  git pull <remote repo> <remote branch>:<local branch>
  ```
  <a>git pull = git fetch + merge</a>
### git push
Push the local repo to branch **master** of remote repo **origin**
```commandline
git push -u origin master
```

