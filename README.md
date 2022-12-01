
- This is a Makefile target to push to `main` / `master`...
  - Left-hand tabs are requried... vim can mess that up if you translate tabs to spaces in vim
  - Use `ping` as a basic internet connectivity test
  - This `Makefile` captures the `main` / `master` branch name

```Makefile
.DEFAULT_GOAL := git-push

.PHONY: git-push
git-push:
	@echo ">> checkout master branch, push to origin/master, switch back to develop"
	ping -q -c1 -W1 4.2.2.2                   # ensure the internet is connected
	-git checkout master || git checkout main # Add dash to ignore checkout fails
	THIS_BRANCH=$(shell git branch --show-current)  # ENV var assignment, no space
	git merge @{-1}                           # merge the previous branch (@{-1})
	git push origin $(THIS_BRANCH)            # push to origin/master...
	git checkout @{-1}                        # checkout the previous branch...
```
