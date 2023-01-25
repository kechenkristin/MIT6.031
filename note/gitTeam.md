## reference
Author: Programmer who can play the guitar  
Link: https://juejin.cn/post/6976633078714204167  
Source: Rare Earth Nuggets  
Copyright belongs to the author. For commercial reprint, please contact the author for authorization, for non-commercial reprint, please indicate the source.

## Instruction
1. master - master branch
- All official versions available to users are released on this master branch
- Developers are not allowed to push on this branch

2. dev - the development branch
- The branch used for daily development, the phased functional modules completed by developers will be merged into this branch first
- This branch is also the branch used by the team for internal testing and phased work verification
- Developers cannot perform push operations on this branch, and can only merge their personal branches into this branch through Pull Requests
- During development, keep in sync with this branch frequently

3. feature/xxx - feature branch
- For the development of a certain functional module, for example: Zhang San created a feature/package-manager branch responsible for developing the package manager module

- When the development task of the functional module is completed, the pull request will be merged in the form of a pull request. After the administrator's Code Review is passed, the branch will be merged into the dev branch; after that, the branch will be deleted

- Once developed, they are merged into the dev branch **(only via Pull Request)** and then deleted

- Such branches are managed and used by developers personally and can be pushed
During development, such branches should always be kept in sync with the dev branch

4. hotfix/xxx - patch branch
- Branches for emergency bug fixes, can be created from master or dev branches

- As with feature/xxx branches, once fixes are done, they are merged into master or dev branch (only via Pull Request) and then deleted

## work flow
### Before Development
- fork repo

- clone dev branch into local
```
git clone -b dev https://github.com/liangpengyv/vue-mvvm.git
```

### Step 1: Create New Branch
- get the newest codes of dev branch
```
git checkout dev
git pull
```

- create a new feature branch
```
git branch feature/xxx
```

- checkout to the new feature branch to development
```
git checkout feature/xxx
```

### Step 2: Commit Branch
After the branch is modified, it can be submitted

- commit code
```
git add .
git commit -m "leave your message here
```

- During the development process, push the feature branch in the development of the local warehouse to the remote warehouse (optional)
```
git push -u origin feature/xxx
```

### Step 3: Sync with dev branch
During the development of the branch, it is necessary to keep in sync with the dev branch frequently

- Get the latest code from the dev branch
```
git checkout dev
git pull
```

- Switch back to the currently developed feature branch
```
git checkout feature/xxx
```

- Merge dev branch into current branch
```
git merge dev
```

### Step4 : Pull Request
After completing all the development tasks of the current feature branch, performing the last **synchronization with the dev trunk**, and submitting it to the remote repo, you can issue a **Pull Request** to the **dev branch**, and then request the administrator to conduct a **Code Review** to confirm that it can be merged into the dev branch.

- Finally, perform the synchronization work of step 3

- Submit to remote repository
```
git checkout feature/xxx
git push origin feature/xxx
```

- Create a Pull Request in the GitHub management interface and wait for the administrator to conduct a Code Review

### Step 5: Clean up useless branches
After the development tasks of a feature branch are all completed, it should be deleted.

- First, switch back to the dev branch
```
git checkout dev
```

- Delete the remote feature branch first
```
git push origin -d feature/xxx
```

- Then delete the local feature branch
```
git branch -d feature/xxx
```
