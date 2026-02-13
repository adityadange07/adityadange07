
## 881. What is Git?

**Answer:**
**Git** is a distributed version control system (DVCS) used to track changes in source code.
*   **Distributed:** Every developer has a full copy of the repository (history + code) on their local machine.
*   **Goal:** Enable collaboration, history tracking, and reverting changes.

---

## 882. What is commit?

**Answer:**
A **Commit** is a snapshot of the project's files at a specific point in time.
*   **Properties:**
    *   **SHA-1 Hash:** Unique ID (e.g., `a1b2c3d`).
    *   **Message:** Description of the change.
    *   **Author/Date:** Who and When.
    *   **Parent:** Link to the previous commit (forming a chain).

---

## 883. What is branch?

**Answer:**
A **Branch** is a lightweight pointer to a specific commit.
*   **Purpose:** Allows you to diverge from the main line of development (e.g., `main`) to work on a feature or bug fix in isolation.
*   **Head:** A pointer to the *current* branch you are working on.

---

## 884. What is merge?

**Answer:**
**Merge** takes the contents of a source branch and integrates them with a target branch.
*   **Fast-Forward:** If no divergent work exists, just move the pointer forward.
*   **True Merge (3-Way):** If divergent work exists, creates a new **Merge Commit** with two parents.

---

## 885. What is rebase?

**Answer:**
**Rebase** moves or combines a sequence of commits to a new base commit.
*   **Process:** It takes your changes and "plays" them on top of the latest version of the target branch.
*   **Goal:** Maintains a linear project history (no ugly merge bubbles).

---

## 886. Merge vs rebase difference?

**Answer:**
*   **Merge:** Preserves history exactly as it happened. Creates an extra commit (Merge Commit) if branches diverged. Safe for shared branches.
*   **Rebase:** Rewrites history to make it linear. Cleaner, but dangerous on shared branches (changes Commit IDs).

---

## 887. What is cherry-pick?

**Answer:**
**Cherry-Pick** applies the changes introduced by some existing commits (from another branch) onto the current branch.
*   **Use Case:** You fixed a critical bug in `dev` and want to apply *only* that specific commit to `prod` without merging the entire `dev` branch.

---

## 888. What is stash?

**Answer:**
**Stash** temporarily shelves (saves) changes you've made to your working copy so you can work on something else, and then come back and re-apply them later.
*   **Command:** `git stash` (save), `git stash pop` (restore).
*   **Scenario:** You are working on a feature, but need to switch branches to fix a bug immediately, but your code isn't ready to commit.

---

## 889. What is reset?

**Answer:**
**Reset** moves the current branch pointer backward to a specific commit.
*   **Soft:** `git reset --soft HEAD~1` (Moves pointer back, keeps changes in Staging Area).
*   **Mixed:** (Default) Moves pointer back, keeps changes in Working Directory (Unstaged).
*   **Hard:** `git reset --hard HEAD~1` (Moves pointer back, **destroys** all changes).

---

## 890. What is revert?

**Answer:**
**Revert** creates a *new* commit that undoes the changes made in a previous commit.
*   **Difference from Reset:** It adds to history instead of rewriting it.
*   **Safe:** This is the correct way to undo changes on a **public/shared** branch.

---

## 891. What is detached HEAD?

**Answer:**
**Detached HEAD** state occurs when you check out a specific **Commit SHA** instead of a Branch name.
*   **State:** HEAD points directly to a commit, not a branch reference.
*   **Risk:** Any new commits made in this state will be "orphaned" (lost) when you switch away, unless you create a new branch to save them.

---

## 892. What is squash?

**Answer:**
**Squashing** combines multiple commits into a single commit.
*   **Use Case:** Cleaning up a messy history before merging a Pull Request.
    *   *Before:* "WIP", "Fix typo", "Fixed bug", "Final fix".
    *   *After:* "Implemented Feature X".
*   **Command:** Interactive Rebase (`git rebase -i`).

---

## 893. What is tag?

**Answer:**
A **Tag** is a reference to a specific commit that does not move (unlike a branch).
*   **Purpose:** To mark specific release points (e.g., `v1.0.0`, `v2.1.0`).
*   **Types:**
    *   **Lightweight:** Just a pointer.
    *   **Annotated:** Includes a message, author, and date (stored as a full object).

---

## 894. What is conflict resolution?

**Answer:**
**Merge Conflicts** occur when two branches have modified the same lines in a file, or one deleted a file while another modified it.
*   **Process:**
    1.  Git pauses the merge.
    2.  Developer manually edits the file to choose changes (HEAD vs Incoming).
    3.  Developer adds the file (`git add`) and commits to finish the merge.

---

## 895. What is git workflow models?

**Answer:**
**Git Workflows** define how developers collaborate and use branches.
*   **Common Models:**
    1.  Centralized Workflow (SVN style).
    2.  Feature Branch Workflow.
    3.  GitFlow.
    4.  Trunk-Based Development.

---

## 896. What is GitFlow?

**Answer:**
**GitFlow** is a strict branching model designed around project releases.
*   **Branches:**
    *   `main`: Production code.
    *   `develop`: Integration branch for features.
    *   `feature/*`: Logic for new features.
    *   `release/*`: Prep for a new production release.
    *   `hotfix/*`: Urgent fixes for production.
*   **Cons:** Complex, slow for CI/CD.

---

## 897. What is trunk-based development?

**Answer:**
**Trunk-Based Development** allows developers to merge small, frequent updates to a core "trunk" or "main" branch.
*   **Key:** Avoid long-lived feature branches. Merge daily.
*   **Enabler:** Feature Flags (to hide unfinished code).
*   **Pros:** Minimal merge conflicts, enables true CI/CD.

---

## 898. What is submodule?

**Answer:**
**Submodules** allow you to keep a Git repository as a subdirectory of another Git repository.
*   **Use Case:** Shared library code used by multiple projects.
*   **Mechanic:** The parent repo tracks the specific **Commit SHA** of the submodule, not the branch tip.

---

## 899. What is hook?

**Answer:**
**Git Hooks** are scripts that run automatically before or after Git events.
*   **Client-Side:**
    *   `pre-commit`: Run linters/tests before allowing a commit.
    *   `pre-push`: Prevent pushing secrets.
*   **Server-Side:**
    *   `pre-receive`: Enforce rules on the server (e.g., commit message format).

---

## 900. What is shallow clone?

**Answer:**
**Shallow Clone** pulls only the latest history (or a specific depth) instead of the entire project history.
*   **Command:** `git clone --depth 1 <url>`.
*   **Use Case:** CI/CD pipelines (faster download speed since history isn't needed for building).

---

## 901. What is bisect?

**Answer:**
**Git Bisect** is a debugging tool that uses excessive binary search to find which specific commit introduced a bug.
*   **Process:**
    1.  Start bisect: `git bisect start`.
    2.  Mark current commit as bad: `git bisect bad`.
    3.  Mark an older commit as good: `git bisect good <sha>`.
    4.  Git checks out the middle commit -> You test -> Mark good/bad -> Repeats until the culprit is found.

---

## 902. What is blame?

**Answer:**
**Git Blame** shows what revision and author last modified each line of a file.
*   **Command:** `git blame <filename>`.
*   **Use Case:** Identifying who wrote a specific piece of logic or when it was changed, to ask for context (not just for "blaming").

---

## 903. What is reflog?

**Answer:**
**Reflog** (Reference Log) records updates to the tip of branches and other references (HEAD).
*   **Superpower:** It allows you to recover **"lost" commits** (e.g., after a hard reset or deleted branch) that are no longer referenced by any branch but are still in the local object database.
*   **Command:** `git reflog`.

---

## 904. How to recover deleted branch?

**Answer:**
If you accidentally deleted a branch that wasn't merged:
1.  Run `git reflog` to find the SHA of the commit the branch pointed to before deletion.
2.  Recreate the branch pointing to that SHA: `git checkout -b <branch-name> <sha>`.

---

## 905. How to revert pushed commit?

**Answer:**
*   **Private Branch:** `git reset --hard HEAD~1` then `git push --force` (Dangerous).
*   **Shared/Public Branch:** `git revert <sha>`. This creates a *new* commit that is the strict inverse of the bad commit. This is safe for history.

---

## 906. How to resolve large repo issue?

**Answer:**
Repositories get slow if large binary files (jars, images) are committed along with code.
*   **Solution:** Use **Git LFS (Large File Storage)**.
    *   Replaces large files with text pointers inside Git.
    *   Stores the actual file contents on a separate server (e.g., S3).
    *   Downloaded only when needed (lazy fetch).

---

## 907. How to manage versioning?

**Answer:**
Versioning creates unique identifiers for different states of source code.
*   **Tags:** Use Git Tags to mark release points.
*   **Strategy:** Follow a standard schema like **SemVer** to communicate compatibility.

---

## 908. What is semantic versioning?

**Answer:**
**Semantic Versioning (SemVer)** uses `MAJOR.MINOR.PATCH` (e.g., `2.1.4`).
1.  **MAJOR:** Incompatible API changes (Breaking changes).
2.  **MINOR:** Add functionality in a backwards-compatible manner (New features).
3.  **PATCH:** Backwards-compatible bug fixes.

---

## 909. What is code review best practice?

**Answer:**
1.  **Small PRs:** Easier to review (< 400 lines).
2.  **Linting:** Automate style checks (don't waste human time on formatting).
3.  **Context:** Provide a clear description and screenshots.
4.  **Tone:** Be constructive ("Could we try..." instead of "Wrong").
5.  **Turnaround:** Review within 24 hours to enable flow.

---

## 910. What is pull request strategy?

**Answer:**
Defining how changes are merged.
1.  **Merge Commit:** Keeps full history. Good for feature branches.
2.  **Squash and Merge:** One commit per PR. Keeps main history clean. (Preferred by many).
3.  **Rebase and Merge:** Linear history, but individual commits are preserved.
