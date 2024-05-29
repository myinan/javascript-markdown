# Using Git in the Real World
## Git Workflow for Open Source Contribution

### Initial Setup

1. Read the contributing guide for the project.
2. Fork the original ("upstream") repository on Github.
3. Clone your forked repository to your local machine:
   ```bash
   git clone git@github.com:your_user_name_here/forked_repo.git
   ```
4. Add a remote named "upstream" pointing to the original repository:
   ```bash
   cd forked_repo
   git remote add upstream git@github.com:original_repo_owner/original_repo.git
   ```

### Ongoing Workflow

1. Create a new feature branch for your work:
   ```bash
   git checkout -b your_feature_name
   ```

2. Add and commit changes following best practices.

3. Fetch the most updated changes from the original repository:
   ```bash
   git fetch upstream
   ```

4. Merge upstream changes into your local main branch:
   ```bash
   git checkout main
   git merge upstream/main
   ```

   Note: This is equivalent to `git pull upstream main`.

5. Switch back to your feature branch and merge main into it:
   ```bash
   git checkout your_feature_name
   git merge main
   ```

   Resolve any merge conflicts if needed.

6. Now your feature branch is clean and up-to-date.

### Sending Your Pull Request

1. Push your feature branch to your fork on GitHub:
   ```bash
   git push origin your_feature_name
   ```

2. Submit a pull request using GitHub's interface:
   - Visit your fork on GitHub.
   - Switch to the branch you want to merge.
   - Click on "New Pull Request" and follow the prompts.

3. Submit the pull request to merge your feature branch into the original upstream repository’s main branch.

Congratulations! You've successfully contributed to an open source project. 🚀

---
### Knowledge Check

**Q1.** What name is typically given for a Git remote that points to a repo that’s been forked?

**A1.** The original repository that we have forked from is usually called `upstream`.

**Q2.** Can you directly send your changes to a repository that you don’t own/have write access to?

**A2.** On Github, we can't direcly make changes to a repository we do not have write access to. Instead, we can create a pull request that involves our changes, and the owner of the original repository will have to decide whether or not to incorporate those changes into the upsteam repository.

**Q3.** What should you do immediately before merging your feature branch into main?

**A3.** Since we are working on the local clone of the forked repo, the upstream/original repo may have changes made to it while we were working on our feature locally. So in order to prevent version conflicts between our fork and the upstream, we should feth-merge/pull the original upstream repository from our local clone, so that we make sure we are up to date with the upstream.