# squash-merge-test
Test of GitHub's "squash and merge" functionality to see what the git history looks like

## Method

1. Create this repo, with a README so there is an initial commit
2. Clone repo locally
3. Make a branch with a few commits
   ```bash
   git checkout -b "multi-commit-branch"
   git commit --allow-empty -m "branch-commit-1"
   git commit --allow-empty -m "branch-commit-2"
   git commit --allow-empty -m "branch-commit-3"
   git push origin "multi-commit-branch"
   ```
4. Make a pr with the branch
   ```bash
   gh pr create \
       --base "main" \
       --head "multi-commit-branch" \
       --title "Multi commit branch" \
       --body "To be squashed+merged"
   ```
5. Open PR in GitHub UI and change the "Merge pull request" dropdown to "Squash and merge" then hit the button
6. Fetch changes locally and inspect the log
   ```bash
   git checkout main
   git fetch --all
   git log --graph --decorate --all --online | cat
   ```
   
   ```
   * 4e08223 (origin/main, origin/HEAD) Multi commit branch (#1)
   | * 91768e4 (origin/multi-commit-branch, multi-commit-branch) branch-commit-3
   | * 7ed0a6e branch-commit-2
   | * e01e030 branch-commit-1
   |/  
   * 207dae5 (HEAD -> main) Initial commit
   ```
