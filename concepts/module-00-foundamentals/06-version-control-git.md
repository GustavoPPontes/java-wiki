## What Version Control Is

Version control is a system that records changes to files over time. Each modification is tracked, timestamped, and attributed to whoever made it. You can revisit any previous state of your project, compare versions, and restore something you deleted three weeks ago.

Think of it as a detailed, automatic logbook for your codebase. Every save point, called a **commit**, captures a snapshot of the project at a specific moment. The full chain of commits forms the project's **history**: a complete, navigable timeline of what changed, when, and by whom.

Version control operates on **repositories** (or **repos**). A repository is the container that holds all your project's files together with their entire change history. It can live on your machine (local) or on a remote server shared with your team.

## Why It Exists

Software is written incrementally. Features are added, bugs are fixed, experiments are tried and discarded. Without a system to track those changes, collaboration between developers becomes a minefield of overwritten files, lost work, and unrecoverable mistakes.

Before version control, teams resorted to copying folders, naming them `project_v2_final_FINAL`, and praying no one edited the wrong file. This approach does not scale. It breaks with two people; it collapses with twenty.

Version control solves three problems at once: it preserves history, it enables parallel work, and it provides a mechanism to merge divergent changes back together. The first gives you safety. The second gives you speed. The third gives you collaboration without chaos.

## Git vs GitHub

Git is a **distributed version control system**. Created for the Linux kernel and now the de facto standard, it gives every contributor a full local copy of the repository, including its complete history. Commits, branching, merging, and diffs all happen locally and fast, then sync to a shared remote when you are ready.

Git is a command-line tool. It runs on your machine. It does not need the internet to function: you can commit, branch, and inspect history while offline.

GitHub is a **web platform** built on top of Git. GitHub is a web-based developer platform for version control, code hosting, and software collaboration. Founded in 2008 and acquired by Microsoft in 2018, GitHub is built around Git, a distributed version control system. GitHub adds collaboration features such as pull requests, issues, discussions, project boards, and CI/CD automation via GitHub Actions.

The distinction matters: Git is the engine, GitHub is a service that hosts your Git repositories and wraps them in a collaboration layer. Platforms like GitHub, GitLab, and Bitbucket are not alternatives to Git; they sit on top of Git and add hosting, code review, permissions, and CI/CD around it. You can use Git without GitHub. You cannot use GitHub without Git.

## The Basic Workflow

The day-to-day cycle with Git follows a predictable sequence:

1. **Clone** or **init**: You either clone an existing remote repository to your machine (`git clone`) or initialize a new one locally (`git init`).
2. **Modify**: You edit files, write code, fix bugs. Git does not track these changes automatically.
3. **Stage**: You select which changes to include in your next commit by adding them to the **staging area** (`git add`). This is a deliberate step: you choose what goes in and what stays out.
4. **Commit**: You save the staged changes as a snapshot with a descriptive message (`git commit`). The commit is recorded in your local history.
5. **Push**: You send your local commits to a remote repository (`git push`), making them available to the rest of the team.
6. **Pull**: You download and integrate changes others have pushed (`git pull`), keeping your local copy in sync.

This cycle (modify, stage, commit, push) repeats throughout the life of a project. The staging area is what distinguishes Git from simpler systems: it forces you to be intentional about what you record.

## What a Branch Is

A branch is an independent line of development. It lets you diverge from the main codebase, work on something in isolation, and merge the result back when it is ready.

By default, every Git repository starts with a single branch, typically called `main`. When you create a new branch, Git does not copy all your files, it simply creates a pointer to the current commit. This makes branching almost instant and extremely cheap in terms of storage.

Branches exist because parallel work is the norm, not the exception. One developer fixes a bug. Another builds a feature. A third experiments with a refactor that might not survive the week. Each works on their own branch without interfering with anyone else, without risking the stability of the main codebase.

When the work is done, the branch is **merged** back into `main`. If two branches modified the same lines in the same file, Git flags a **merge conflict** and asks you to resolve it manually. Otherwise, the merge is automatic.

Git's strength is workflow flexibility. Lightweight branching makes it cheap to spin up a branch per feature, per fix, or per experiment, then merge back with conflict resolution rather than silent overwrites.

The typical convention: `main` stays stable and deployable. All active work happens on branches. Code enters `main` only after review, usually through a **pull request** on platforms like GitHub, where teammates can inspect, discuss, and approve the changes before they land.

