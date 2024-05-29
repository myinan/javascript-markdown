# A Deeper Look at Git
## Changing Git History
So let’s say you’re comfortable writing good commit messages and you’re working with branches to have a good Git workflow going. But nobody is perfect, and as you’re writing some beautiful code something goes wrong! Maybe you commit too early and are missing a file. Maybe you mess up one of your commit messages and omit a vital detail.

Let’s look at some ways we can change recent and distant git history to fit our needs. We’re going to cover how to:
+ Change our most recent commit
+ Change multiple commit messages
+ Reorder commits
+ Squash commits together
+ Split up commits

**Important:** Changing Git history involves rewriting commits, and it's important to note that doing this on commits that have already been pushed to a shared repository can cause issues for collaborators. So, be cautious when modifying shared history.

### 1. `Change the Most Recent Commit`:

#### Amend the Last Commit:
The `git commit --amend` command is used to modify the most recent Git commit. It allows you to make changes to the commit message or add additional changes to the existing commit. This can be useful if you realize that you forgot to include some changes or if you want to reword the commit message.

Here's a step-by-step explanation of how `git commit --amend` works:

1. **Make Changes:** First, make the necessary changes to your files that you want to include in the amended commit. You can add new files, modify existing ones, or even remove files.

2. **Stage Changes:** Stage the changes you want to include in the amended commit using the `git add` command.

   ```bash
   git add <file1> <file2> ...
   ```

3. **Run `git commit --amend`:** Once the changes are staged, run the `git commit --amend` command:

   ```bash
   git commit --amend
   ```

   This opens the default text editor where you can modify the commit message. If you only want to change the commit message, you can skip the previous `git add` step.

4. **Edit Commit Message (Optional):** If you want to change the commit message, modify the text in the editor. Save and close the editor.

5. **Save Changes:** If you've made changes to the commit message or added new changes, Git will create a new commit object with the updated information.

   - If you only modified the commit message, the existing commit will be updated with the new message.
   - If you added new changes, a new commit will be created, and the branch will be updated to point to this new commit.

6. **Push the Changes (Optional):** If the branch with the amended commit has already been pushed to a remote repository, you might need to force-push the changes, especially if the commit you amended has already been pushed. Be cautious with force-pushing, as it can overwrite the commit history and cause issues for collaborators.

   ```bash
   git push origin <branch-name> --force
   ```

### 2. `Change Multiple Commit Messages`:

#### Interactive Rebase:
Changing multiple commit messages in Git can be done using an interactive rebase. This process involves rewriting the commit history, so it should be used with caution, especially if the commits have already been shared with others. Here's a step-by-step guide:

1. **Open Terminal or Command Prompt:**
   Open a terminal or command prompt where your Git repository is located.

2. **Start Interactive Rebase:**
  `git rebase <base>` is used to rebase the current branch onto `<base>`. `<base>` can be a commit ID, branch name, a tag, or a relative reference to HEAD.

   Run the following command to start an interactive rebase:

   ```bash
   git rebase -i HEAD~n
   ```

   Replace `n` with the number of commits you want to modify. If you want to modify the last 3 commits, use `HEAD~3`.

3. **Editor Opens:**
   Git will open an interactive rebase editor, listing the commits you specified. It might look something like this:

   ```bash
   pick abcd123 Commit message 1
   pick efgh456 Commit message 2
   pick ijkl789 Commit message 3
   ```

4. **Change "pick" to "reword":**
   Change the word `pick` to `reword` for each commit whose message you want to modify:

   ```bash
   reword abcd123 Commit message 1
   reword efgh456 Commit message 2
   reword ijkl789 Commit message 3
   ```

5. **Save and Close Editor:**
   Save the changes and close the editor.

6. **Modify Commit Messages:**
   For each commit marked for rewording, Git will prompt you to modify the commit message. The editor will open for each commit individually.

7. **Save and Close Editor (for each commit):**
   In each editor, modify the commit message, save, and close the editor.

8. **Complete the Rebase:**
   After modifying all the commit messages, complete the rebase:

   ```bash
   git rebase --continue
   ```

   If conflicts arise during the rebase, Git will pause and allow you to resolve them.

9. **Force Push (Optional):**
   If you have already pushed the commits to a remote repository, you may need to force-push the changes:

   ```bash
   git push origin <branch-name> --force
   ```

### 3. `Reorder Commits`:

#### Interactive Rebase:
Reordering commits in Git can be done using an interactive rebase. Here's a step-by-step guide:

1. **Open Terminal or Command Prompt:**
   Open a terminal or command prompt where your Git repository is located.

2. **Start Interactive Rebase:**
   Run the following command to start an interactive rebase:

   ```bash
   git rebase -i HEAD~n
   ```

   Replace `n` with the number of commits you want to reorder. If you want to reorder the last 3 commits, use `HEAD~3`.

3. **Editor Opens:**
   Git will open an interactive rebase editor, listing the commits you specified. It might look something like this:

   ```bash
   pick abcd123 Commit message 1
   pick efgh456 Commit message 2
   pick ijkl789 Commit message 3
   ```

4. **Reorder Commits:**
   To change the order of commits, simply change the order of lines in the editor. Move the lines to the desired order. For example:

   ```bash
   pick ijkl789 Commit message 3
   pick efgh456 Commit message 2
   pick abcd123 Commit message 1
   ```

   This will reorder the commits as specified.

5. **Save and Close Editor:**
   Save the changes and close the editor.

6. **Complete the Rebase:**
   After reordering, complete the rebase:

   ```bash
   git rebase --continue
   ```

   If conflicts arise during the rebase, Git will pause and allow you to resolve them.

7. **Force Push (Optional):**
   If you have already pushed the commits to a remote repository, you may need to force-push the changes:

   ```bash
   git push origin <branch-name> --force
   ```

   Be cautious with force-pushing, as it can rewrite history and cause issues for collaborators.

Keep in mind that reordering commits changes the commit IDs, and this can cause problems for collaborators if the branch has already been pushed.

### 4. `Squash Commits Together`:

#### Interactive Rebase:
Squashing commits in Git involves combining multiple commits into a single, larger commit. This is useful for cleaning up a branch's commit history and making it more concise. The process is typically done using an interactive rebase. Here's a step-by-step guide:

1. **Open Terminal or Command Prompt:**
   Open a terminal or command prompt where your Git repository is located.

2. **Start Interactive Rebase:**
   Run the following command to start an interactive rebase:

   ```bash
   git rebase -i HEAD~n
   ```

   Replace `n` with the number of commits you want to squash. If you want to squash the last 3 commits, use `HEAD~3`.

3. **Editor Opens:**
   Git will open an interactive rebase editor, listing the commits you specified. It might look something like this:

   ```bash
   pick abcd123 Commit message 1
   pick efgh456 Commit message 2
   pick ijkl789 Commit message 3
   ```

4. **Mark Commits for Squashing:**
   To squash commits, change the word `pick` to `squash` (or just `s`) for the commits you want to combine:

   ```bash
   pick abcd123 Commit message 1
   squash efgh456 Commit message 2
   squash ijkl789 Commit message 3
   ```

   The commit marked as `pick` will be the base commit, and the others will be squashed into it.

5. **Save and Close Editor:**
   Save the changes and close the editor.

6. **Edit Combined Commit Message (Optional):**
   After saving, another editor will open to allow you to edit the commit message for the combined commit. If you want to keep a summary of the original commit messages, you can include them in the new message.

7. **Save and Close Editor:**
   Save the changes and close the editor.

8. **Complete the Rebase:**
   After squashing, complete the rebase:

   ```bash
   git rebase --continue
   ```

   If conflicts arise during the rebase, Git will pause and allow you to resolve them.

9. **Force Push (Optional):**
   If you have already pushed the commits to a remote repository, you may need to force-push the changes:

   ```bash
   git push origin <branch-name> --force
   ```

### 5. `Split Up Commits`:

#### Interactive Rebase:
Splitting up commits in Git is a way to divide a single commit into multiple smaller commits. This is useful when you realize that a commit contains changes that should have been separate. To split a commit, you need to use an interactive rebase. Here's a step-by-step guide:

1. **Open Terminal or Command Prompt:**
   Open a terminal or command prompt where your Git repository is located.

2. **Start Interactive Rebase:**
   Run the following command to start an interactive rebase:

   ```bash
   git rebase -i HEAD~n
   ```

   Replace `n` with the number of commits you want to modify. If you want to modify the last 3 commits, use `HEAD~3`.

3. **Editor Opens:**
   Git will open an interactive rebase editor, listing the commits you specified. It might look something like this:

   ```bash
   pick abcd123 Commit message 1
   pick efgh456 Commit message 2
   pick ijkl789 Commit message 3
   ```

4. **Mark Commit for Editing:**
   Change the word `pick` to `edit` for the commit you want to split:

   ```bash
   edit abcd123 Commit message 1
   pick efgh456 Commit message 2
   pick ijkl789 Commit message 3
   ```

   Save and close the editor.

5. **Make Changes:**
   After marking the commit for editing, Git will stop at that commit during the rebase process. Now, you can use the following commands to uncommit the changes and stage only the changes you want in the first commit:

   ```bash
   git reset HEAD^      # Uncommit changes
   git add -p           # Stage only the changes you want
   ```

   The `-p` flag allows you to interactively stage changes.

6. **Commit the First Part:**
   Commit the changes you've staged:

   ```bash
   git commit -m "First part of changes"
   ```

7. **Repeat Steps for Remaining Changes:**
   Repeat steps 3 to 6 for each part of the changes you want in separate commits. Use the `git rebase --continue` command to proceed after each commit.

8. **Complete the Rebase:**
   After splitting the commits, complete the rebase:

   ```bash
   git rebase --continue
   ```

   If conflicts arise during the rebase, Git will pause and allow you to resolve them.

9. **Force Push (Optional):**
   If you have already pushed the commits to a remote repository, you may need to force-push the changes:

   ```bash
   git push origin <branch-name> --force
   ```

## The Commit History Structure and Branches
In Git, the commit history is represented as a directed acyclic graph (DAG). Each commit in a Git repository points to its parent commit or commits, forming a chain of commits. Since there are no cycles in this structure, it is a directed acyclic graph.

The parent-child relationships between commits are what create the branching and merging patterns in Git. Branches are essentially just pointers to specific commits, and when a new commit is made, it points back to its parent commit, creating a new node in the graph.

This DAG structure allows Git to efficiently track the history of changes, branches, and merges, making it a powerful and flexible version control system.

  1. **Commits:**
    - In Git, a commit represents a snapshot of the project at a specific point in time.
    - Each commit has a unique identifier called a hash, which is a cryptographic checksum generated based on the content of the commit.

  2. **Directed Acyclic Graph (DAG):**
    - The commit history is organized as a directed acyclic graph.
    - "Directed" means that there are arrows pointing from one commit to another, representing the parent-child relationship.
    - "Acyclic" means that there are no cycles in the graph, i.e., you cannot follow a sequence of commits that ultimately loops back to the starting commit.

  3. **Parent-Child Relationships:**
    - Each commit points to its parent commit(s).
    - In a simple linear history, each commit has one parent (except for the initial commit, which has none).
    - In the case of a merge, a commit can have multiple parents, representing the merging of different branches.

  4. **Branches and Head:**
    - A branch in Git is essentially a movable pointer to a commit.
    - The special pointer called `HEAD` always points to the latest commit in the currently checked-out branch.
    - When you create a new commit, the branch pointer and `HEAD` move forward to the new commit.

  5. **Merging:**
    - When you merge two branches, a new commit is created with multiple parents (one for each branch being merged).
    - This merge commit represents the point where the branches come together.

  6. **Branching:**
    - Creating a new branch is like creating a new pointer to an existing commit.
    - Commits made on a branch only affect that branch until a merge occurs.

  7. **Tagging:**
    - Git allows you to tag specific commits with a tag name (like a release version).
    - Tags are fixed references that do not move with new commits.

In summary, the commit history in Git is a DAG where each commit points to its parent(s), forming a graph structure. This structure allows Git to track changes, branch off, merge back together, and maintain a complete history of the project. The acyclic nature ensures a clear linear progression of changes over time.

## `git reset`
The `git reset` command is a powerful and flexible tool in Git that allows you to move the current branch pointer to a different commit, effectively resetting the current branch to that commit. This command can be used to undo changes, unstage files, and manipulate the commit history.

The basic syntax for `git reset` is as follows:

```bash
git reset [options] [commit]
```

Here, `[options]` can be different configurations that control the behavior of the reset, and `[commit]` is the commit to which you want to move the branch pointer. If `[commit]` is omitted, it defaults to the last commit in the current branch.

Here are the most commonly used options with `git reset`:

1. **--soft:**
   - This option resets the current branch pointer to the specified commit but leaves the changes staged. It means the changes made in the commits after the specified commit will be kept as uncommitted changes in the working directory.

   ```bash
   git reset --soft [commit]
   ```

2. **--mixed (default):**
   - This is the default option if none is specified. It resets the current branch pointer to the specified commit and unstages the changes. The changes made in the commits after the specified commit will be kept as uncommitted changes in the working directory.

   ```bash
   git reset --mixed [commit]
   ```

3. **--hard:**
   - This option resets the current branch pointer to the specified commit and discards all changes in the working directory and staging area made after that commit. It effectively removes all commits made after the specified commit.

   ```bash
   git reset --hard [commit]
   ```

4. **--merge:**
   - This option is used to undo a failed merge. It resets the current branch pointer to the specified commit and preserves changes in the working directory and staging area. It is often followed by additional actions to resolve the failed merge.

   ```bash
   git reset --merge [commit]
   ```

5. **--keep:**
   - This option is similar to `--hard`, but it will refuse to reset if there are uncommitted changes in the working directory. It's a safer option to avoid accidental data loss.

   ```bash
   git reset --keep [commit]
   ```

6. **--quiet (-q):**
   - This option makes the command less verbose by suppressing output messages.

   ```bash
   git reset --hard -q [commit]
   ```

Remember to use the `git reset` command with caution, especially with the `--hard` option, as it can lead to irreversible data loss. Always double-check which commits you are resetting to and make sure you have a backup if necessary.

---
### Knowledge Check

**Q1.** Explain what it means for branches to be pointers.

**A1.** In the context of version control systems, particularly Git, the concept of branches being pointers refers to the idea that a branch is essentially a reference or pointer to a specific commit in the version history of a project. Let's break this down:

1. **Commits:**
   - In version control systems like Git, a commit represents a snapshot of the project at a specific point in time.
   - Each commit has a unique identifier (usually a hash) that distinguishes it from other commits.

2. **Branches:**
   - A branch in Git is a lightweight movable pointer to a commit. When you create a new branch, it points to a specific commit in the project's history.
   - The branch effectively "labels" the commit it points to and any subsequent commits made on that branch.

3. **Pointer Analogy:**
   - Think of a branch as a pointer or reference to the latest commit in a series of commits. As you make new commits on that branch, the branch pointer moves forward to point to the latest commit.

4. **Creating a Branch:**
   - When you create a new branch, it is created based on the commit that the current branch is pointing to. This new branch initially points to the same commit.

5. **Switching Branches:**
   - When you switch between branches, you are essentially moving the pointer to a different commit. This changes the state of your working directory to match the state of the project at the commit the branch is pointing to.

6. **Merging:**
   - When you merge branches, Git combines the changes from different branches by creating a new commit. The branch that you are currently on (the one you want to merge into) will be updated to point to this new commit.

7. **Branching Strategy:**
   - This pointer-based nature of branches allows for flexible branching strategies. Developers can create branches to work on new features, bug fixes, or experimental changes without affecting the main development line until they are ready to merge.

**Q2.** How can you amend your last commit?

**A2.**
#### Amend the Last Commit:
The `git commit --amend` command is used to modify the most recent Git commit. It allows you to make changes to the commit message or add additional changes to the existing commit. This can be useful if you realize that you forgot to include some changes or if you want to reword the commit message.

Here's a step-by-step explanation of how `git commit --amend` works:

1. **Make Changes:** First, make the necessary changes to your files that you want to include in the amended commit. You can add new files, modify existing ones, or even remove files.

2. **Stage Changes:** Stage the changes you want to include in the amended commit using the `git add` command.

   ```bash
   git add <file1> <file2> ...
   ```

3. **Run `git commit --amend`:** Once the changes are staged, run the `git commit --amend` command:

   ```bash
   git commit --amend
   ```

   This opens the default text editor where you can modify the commit message. If you only want to change the commit message, you can skip the previous `git add` step.

4. **Edit Commit Message (Optional):** If you want to change the commit message, modify the text in the editor. Save and close the editor.

5. **Save Changes:** If you've made changes to the commit message or added new changes, Git will create a new commit object with the updated information.

   - If you only modified the commit message, the existing commit will be updated with the new message.
   - If you added new changes, a new commit will be created, and the branch will be updated to point to this new commit.

6. **Push the Changes (Optional):** If the branch with the amended commit has already been pushed to a remote repository, you might need to force-push the changes, especially if the commit you amended has already been pushed. Be cautious with force-pushing, as it can overwrite the commit history and cause issues for collaborators.

   ```bash
   git push origin <branch-name> --force
   ```


**Q3.** What are some different ways to rewrite history?

**A3.** 
+ The `git commit --amend` command can be used to modify the most recent Git commit.
+ With interactive rebasing `(git rebase -i HEAD~n)` we can change multiple commit messages, reorder commits, squash commits together and even split up commits.
+ The `git reset` command is a powerful and flexible tool in Git that allows you to move the current branch pointer to a different commit, effectively resetting the current branch to that commit. This command can be used to undo changes, unstage files, and manipulate the commit history.