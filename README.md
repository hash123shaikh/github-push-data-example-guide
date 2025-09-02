# Pushing Data from Local System to GitHub Repository - Guideline

Push any local folder to a new GitHub repo with a few commands.

## 1) Make an empty repo on GitHub

Create a new repo on GitHub named `local-to-github-quickstart`.

Do not add a README or .gitignore in the GitHub UI.  

(If you did add one, the remote is not empty. Step 3 explains how to fix the first push.)


## 2) In your local project folder

Pick SSH or HTTPS for the remote and run these.

```bash
# init and set main
git init                         # start git in the current folder
git branch -M main               # name the default branch "main"

# add remote (pick ONE of these and run only that line)

# SSH:
git remote add origin git@github.com:hash123shaikh/local-to-github-quickstart.git

# HTTPS (use this form if you prefer tokens over SSH keys):
# git remote add origin https://github.com/hash123shaikh/local-to-github-quickstart.git

git remote -v                    # verify the remote URL

# first commit and push
git add .                        # stage all current files
git commit -m "Initial commit"     # save a snapshot with a message
git push -u origin main          # push and set "origin/main" as the upstream
```

What those commands mean (in one line each):

- `git init`: turn this folder into a git repository
- `git branch -M main`: make the primary branch name "main"
- `git remote add origin ...`: connect your local repo to GitHub
- `git add .`: include all current changes in the next commit
- `git commit -m "..."`: record a version with a message
- `git push -u origin main`: upload to GitHub and remember the tracking branch


## 3) If you see "fetch first" on push

This happens when the remote already has a commit (for example, you created the repo with a README in the UI).

Do this once, then push again:

```bash
git pull --rebase origin main    # bring the remote commit into your history
# if a conflict appears, fix the file(s), then:
# git add <fixed-file>
# git rebase --continue
git push -u origin main
```

Why this works: `pull --rebase` downloads the remote commit, then replays your local commit on top. That keeps a clean, linear history.

## Tips

- Check the remote URL: git remote -v
  
- SSH or HTTPS
  
  - SSH avoids repeated logins once your key is added to GitHub (ssh -T git@github.com to test)
  - HTTPS uses a token when Git asks for credentials
    
- Avoid pushing files larger than 100 MB (GitHub blocks them)
  
- Keep sensitive data out of Git
  
- Optional, for large non-sensitive files, use Git LFS:

```bash
git lfs install
git lfs track "*.zip"
git add .gitattributes
```



















