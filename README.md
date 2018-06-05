# git-init

[![Repo on GitHub](https://img.shields.io/badge/repo-GitHub-3D76C2.svg)](https://github.com/MoOx/git-init)
[![Repo on GitLab](https://img.shields.io/badge/repo-GitLab-6C488A.svg)](https://gitlab.com/MoOx/git-init)
[![Repo on BitBucket](https://img.shields.io/badge/repo-BitBucket-1F5081.svg)](https://bitbucket.org/MoOx/git-init)

> Keep in sync your Git repos on GitHub, GitLab & Bitbucket without efforts

**Once** Install some CLI tools

```console
brew install hub
gem install gitlab
pip install bitbucket-cli
```

Note: be sure to have tokens as env var, see the beginning of this post for
details.

(Also, configure a git alias that will do `pull --all` if you want to pull all
remote by default.)

### For each repos

1.  Export your username (assuming you have the same on all platforms)

```console
export GIT_USER_NAME=$USER
```

2.  For new repo (if your repo already exist on GitHub, go to step below.)

```console
export GIT_REPO_NAME=your-repo
mkdir $GIT_REPO_NAME && cd $GIT_REPO_NAME
git init
hub create
```

3.  For existing GitHub repo

```console
export GIT_REPO_NAME=$(basename $(pwd))
gitlab create_project $GIT_REPO_NAME "{visibility_level: 20}"
bb create --protocol=ssh --scm=git --public $GIT_REPO_NAME
```

Then, to add remotes

```
git remote set-url origin --add https://gitlab.com/${GIT_USER_NAME}/${GIT_REPO_NAME}.git
git remote set-url origin --add https://bitbucket.org/${GIT_USER_NAME}/${GIT_REPO_NAME}.git
git remote add origin-gitlab https://gitlab.com/${GIT_USER_NAME}/${GIT_REPO_NAME}.git
git remote add origin-bitbucket https://bitbucket.org/${GIT_USER_NAME}/${GIT_REPO_NAME}.git
```

4.  Check that everything is ok

```console
git remote -v
```

You should get something like

```
origin  ssh://git@github.com/YOU/YOUR-REPO.git (fetch)
origin  ssh://git@github.com/YOU/YOUR-REPO.git (push)
origin  ssh://git@gitlab.com/YOU/YOUR-REPO.git (push)
origin  ssh://git@bitbucket.org/YOU/YOUR-REPO.git (push)
origin-bitbucket        ssh://git@bitbucket.org/YOU/YOUR-REPO.git (push)
origin-bitbucket        ssh://git@bitbucket.org/YOU/YOUR-REPO.git (fetch)
origin-gitlab   ssh://git@gitlab.com/YOU/YOUR-REPO.git (fetch)
origin-gitlab   ssh://git@gitlab.com/YOU/YOUR-REPO.git (push)
```

😇 Now you can just `git push` and `git pull --all`!

## Bonus: badges

You can add some nices badges to show the redundancy on your project README

```markdown
[![Repo on GitHub](https://img.shields.io/badge/repo-GitHub-3D76C2.svg)](https://github.com/YOU/YOUR-REPO)
[![Repo on GitLab](https://img.shields.io/badge/repo-GitLab-6C488A.svg)](https://gitlab.com/YOU/YOUR-REPO)
[![Repo on BitBucket](https://img.shields.io/badge/repo-BitBucket-1F5081.svg)](https://bitbucket.org/YOU/YOUR-REPO)
```

**Adjust `YOU/YOUR-REPO` to your need in the markdown**.

It will look like this

[![Repo on GitHub](https://img.shields.io/badge/repo-GitHub-3D76C2.svg)](https://github.com/YOU/YOUR-REPO)
[![Repo on GitLab](https://img.shields.io/badge/repo-GitLab-6C488A.svg)](https://gitlab.com/YOU/YOUR-REPO)
[![Repo on BitBucket](https://img.shields.io/badge/repo-BitBucket-1F5081.svg)](https://bitbucket.org/YOU/YOUR-REPO)
