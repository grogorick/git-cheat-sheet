> notice: statements in \<angle brackets\> are placeholders


create a git alias for lengthy commands  
`git config --global alias.<new-short-command> "<an annoyingly long command that you need to look up every time>"`

nice one-line-per-commit log  
`git log --graph --date-order       --format=format:'%C(cyan)%h%C(reset) - %C(green)(%ad)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(auto)%d%C(reset)'`

log all branches  
`git log --graph --date-order --all --format=format:'%C(cyan)%h%C(reset) - %C(green)(%ad)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(auto)%d%C(reset)'`

count commits between commits  
`git rev-list <old-commit>..<new-commit> --count`

fix upper/lowercase rename (on Windows)  
`git mv <filename> foo`  
`git mv foo <filename>`

word-wise diff  
`git diff --word-dif`  
`git diff --word-diff=color`

character-wise diff  
`git diff --word-diff --color-words=.`

diff ignoring EOL changes  
`git diff --ignore-space-at-eol`

show file content of specific commit  
`git show <commit>:<path/to/file>`

search commits that changed a specific string  
`git log -G"<search string>"`

seach branch for a specific commit hash  
`git branch -a --contains <commit>`

create patch  
`git diff > diff.patch`

apply patch  
`git apply diff.patch`

initial pull only specific branch  
`git clone -b <branchname> --single-branch <repositiory-url>`

add another branch (to a repo with only one cloned)  
`git remote set-branches --add origin <remote-branch>`  
`git fetch origin <remote-branch>:<local-branch>`

add the branch of a pull request (including the --no-ff merge commit) for Azure DevOps
`git fetch origin pull/<pr-number>/merge:pull/<pr-number>`

set default remote for branch  
`git branch --set-upstream-to=<remote>/<branch>`

push to remote branch with different name  
`git push <remote-name> <local-branch>:<remote-branch>`

change message of last (not yet pushed) commit  
`git commit --amend -m "<new description>"`

replace last commit (not yet pushed) with current state of files  
`git add -u`  
`git commit --amend -m "<new description>"`

remove last commit (not yet pushed) but keep the current changes  
`git reset HEAD^`

remove last two commits (not yet pushed) but keep the current changes  
`git reset HEAD~2`

remove last commit (not yet pushed) and restore files from before this commit  
`git reset --hard HEAD^`

copy changes to stash and reset to current revision  
`git stash`

copy changes to stash with a description and reset to current revision  
`git stash save "<description>"`

view stashed changes in detail  
`git show stash`  
`git show stash@{<stash-index>}`

view list of modified files in stash  
`git show stash --name-only`

view stashed changes of a single file  
`git show stash -- <filename>`

reapply changes from last stash  
`git stash apply`

reapply changes of a single file from stash  
`git checkout stash@{<stash-index>} -- <filename>`

reapply and remove changes from stash  
`git stash pop`

remove element 0 from stash  
`git stash drop stash@{<stash-index>}`

revert a single file  
`git checkout -- <filename>`

restore a single file from a specific commit  
`git checkout <commit-identifier> -- <filename>`

restore a file or folder from a recent commit  
`git checkout <commit> -- <file or folder name>`

restore a branch at a specific time (if you don't know the commit hash)  
`git checkout '<branchname>@{2021-01-01 00:00:00}'`

revert all changes to current head commit  
`git reset --hard`

revert to specific commit  
`git reset --hard <commit>`

create branch  
`git branch <branchname> [<commit>]`

switch to branch  
`git checkout <branchname>`

list all branches and their remotes  
`git branch -a -vv`

delete branch (remote and local)  
`git branch --delete <branchname>`  
`git push --delete origin <branchname> `

copy commit from other branch  
`git cherry-pick <commit>`

after commit A add (cherry-pick) multiple commits B..C  
`git reset --hard C`  
`git rebase --onto A B^`

create tag  
`git tag <tag-name> <commit>`

create named tag  
`git tag -a <tag-name> <commit>`

tags pushen  
`git push --tags`

tags auflisten  
`git tag`

delete local tag  
`git tag --delete <tag-name>`

delete remote tag  
`git push --delete origin <tag-name>`

list untracked files  
`git clean -f -n`

delete untracked files  
`git clean -f`

user-commit statistics  
`git shortlog -sn --no-merges`

allow self-signed certificates  
`git config --global http.sslVerify false`

for a single command  
`git -c http.sslVerify=false \<command\>`

try to recover deleted local files (not committed but staged)  
`mkdir RECOVERED ; for b in $(git fsck --lost-found | grep blob | awk '{print $3}'); do git cat-file -p $b > RECOVERED/$b ; done`

add shallow submodule  
`git submodule add <URL> <PATH>`  
`git config -f .gitmodules submodule.<name>.shallow true`

remove submodule  
`git submodule deinit <path_to_submodule>`  
`git rm <path_to_submodule>`  
`git commit-m "Removed submodule"`  
`rm -rf .git/modules/<path_to_submodule>`

ignore tracked file for future commits  
`git update-index --assume-unchanged <filename>`

unignore file  
`git update-index --no-assume-unchanged <filename>`

find commit that deleted a file  
`git log --diff-filter=D -- <path/to/file>`

rewrite commit messages: replace "old string" with "new string" (for commits in my_branch and not in master)  
`git filter-branch --msg-filter 'sed "s/<old string>/<new string>/g"' master..my_branch`

create a new git repository from a subdirectory (IN PLACE OPERATION - make a copy of the original repo!)  
`git filter-branch --subdirectory-filter <subdirectory> -- --all`

create multi-remote  
`git remote add <remote-name> <url-to-first-remote-repo>`  
`git remote set-url --add <remote-name> <url-to-another-remote-repo>`

fetch notes  
`git fetch origin "refs/notes/*:refs/notes/*"`

search the the full history of all files for a string  
`query="<search-string>"; for hash in $(git log -G${query} --format="%h"); do echo; echo $hash; git show $hash | grep --color=always $query; done`
