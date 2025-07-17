# Version Control System (VCS)

A Version Control System records changes to a file or set of files over time so that you can recall specific versions later.

## Types of VCS

### Local Version Control Systems
- **Description**: Simple database that keeps all changes to files under revision control
- **Examples**: RCS (Revision Control System)
- **Pros**: Simple to use, no network required
- **Cons**: Limited collaboration, single point of failure

### Centralized Version Control Systems
- **Description**: Single server contains all versioned files, clients check out files from that central place
- **Examples**: CVS, Subversion (SVN), Perforce
- **Pros**: Everyone knows what everyone else is doing, fine-grained permissions
- **Cons**: Single point of failure, requires network connection, can lose entire project history

### Distributed Version Control Systems
- **Description**: Clients fully mirror the repository, including its full history
- **Examples**: Git, Mercurial, Bazaar
- **Pros**: 
  - No single point of failure
  - Work offline
  - Faster operations
  - Multiple backup copies
- **Cons**: Steeper learning curve, larger repository size

## Why Use Version Control?

- **Track Changes**: See what changed, when, and why
- **Collaboration**: Multiple people can work on the same project
- **Backup**: Safeguard against data loss
- **Experimentation**: Try new features without breaking existing code
- **Rollback**: Revert to previous versions if needed

## Common VCS Operations

- **Commit**: Save a snapshot of your changes
- **Branch**: Create a separate line of development
- **Merge**: Combine changes from different branches
- **Pull/Push**: Synchronize with remote repositories
- **Log**: View history of changes

## Basic Git Commands

### Getting Started
```bash
# Initialize a new Git repository
git init

# Clone an existing repository
git clone <repository-url>

# Check Git configuration
git config --list
```

### Basic Workflow
```bash
# Check status of working directory
git status

# Add files to staging area
git add <filename>          # Add specific file
git add .                   # Add all files

# Commit changes
git commit -m "Your commit message"

# View commit history
git log
git log --oneline          # Compact view
```

### Working with Branches
```bash
# List all branches
git branch

# Create and switch to new branch
git checkout -b <branch-name>

# Switch between branches
git checkout <branch-name>

# Merge branch into current branch
git merge <branch-name>

# Delete branch
git branch -d <branch-name>
```

### Remote Repository Operations
```bash
# Add remote repository
git remote add origin <repository-url>

# Push changes to remote
git push origin <branch-name>

# Pull changes from remote
git pull origin <branch-name>

# Fetch changes without merging
git fetch origin
```

### Viewing and Comparing
```bash
# Show differences in working directory
git diff

# Show differences in staged area
git diff --staged

# Show specific commit
git show <commit-hash>

# View file history
git log --follow <filename>
```

### Undoing Changes
```bash
# Discard changes in working directory
git checkout -- <filename>

# Unstage files
git reset HEAD <filename>

# Undo last commit (keep changes)
git reset --soft HEAD~1

# Undo last commit (discard changes)
git reset --hard HEAD~1
```

### Useful Aliases
```bash
# Add these to your .gitconfig for shortcuts
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.unstage 'reset HEAD --'
```

## Comprehensive Git Example Workflow

This example demonstrates a complete Git workflow with concrete commands and their outputs.

### 1. Initial Setup
```bash
# Create and navigate to project directory
mkdir my-project
cd my-project

# Initialize Git repository
git init
# Output: Initialized empty Git repository in /path/to/my-project/.git

# Check initial status
git status
# Output: On branch main
#         No commits yet
#         nothing to commit (create/copy files and use git add" to track)
```

### 2. Creating and Tracking Files
```bash
# Create some files
echo "# My Project" > README.md
echo "console.log('Hello World');" > app.js
echo "body { color: blue; }" > styles.css

# Check status after creating files
git status
# Output: On branch main
#         No commits yet
#         Untracked files:
#           (use "git add <file>..." to include in what will be committed)
#                 README.md
#                 app.js
#                 styles.css

# Add all files to staging area
git add .

# Check staged changes
git diff --cached
# Output: Shows the differences of all staged files

# Check status again
git status
# Output: On branch main
#         No commits yet
#         Changes to be committed:
#           (use "git rm --cached <file>..." to unstage)
#                 new file:   README.md
#                 new file:   app.js
#                 new file:   styles.css
```

### 3. Making First Commit
```bash
# Commit with conventional commit message
git commit -m "feat: initial project setup with basic files"
# Output: main (root-commit) a1b2c3d] feat: initial project setup with basic files
#          3 changed,3ions(+)
#          create mode 100644ADME.md
#          create mode 100644 app.js
#          create mode10644styles.css

# View commit history
git log
# Output: commit a1c3d400000000000
#         Author: Your Name <your.email@example.com>
#         Date:   Mon Jan112:0 +0000
#         
#             feat: initial project setup with basic files

# View compact log (if git lg alias is configured)
git lg
# Output: a1b2t: initial project setup with basic files
```

### 4. Working with .gitignore
```bash
# Create .gitignore file
echo "node_modules/" > .gitignore
echo "*.log" >> .gitignore
echo ".env" >> .gitignore

# View .gitignore content
cat .gitignore
# Output: node_modules/
#         *.log
#         .env

# Add .gitignore to repository
git add .gitignore
git commit -m "chore: add .gitignore file"
```

### 5. Making Changes and Staging
```bash
# Modify a file
echo "// Updated application code" >> app.js

# Check working directory changes
git diff
# Output: Shows the difference in app.js

# Stage the change
git add app.js

# Check staged changes
git diff --cached
# Output: Shows the staged change in app.js

# Unstage a file
git restore --staged app.js
# Output: (no output, file is unstaged)

# Check status
git status
# Output: Shows app.js as modified but not staged

# Stage again
git add app.js
git commit -m "feat: add application logic"
```

### 6. Comparing Different States
```bash
# Check difference between working directory and HEAD
git diff HEAD
# Output: Shows any uncommitted changes

# Create a new branch for comparison
git branch stable
git checkout stable
# Output: Switched to branch stable

# Make a change on stable branch
echo "// Stable version" > stable.js
git add stable.js
git commit -m "feat:add stable version"

# Switch back to main
git checkout main

# Compare branches
git diff stable
# Output: Shows differences between main and stable branches

# Compare specific files
git diff stable -- app.js
# Output: Shows differences in app.js between branches
```

### 7. Working with Tags and Version Numbers
```bash
# Create lightweight tag for version 1.0.0ag v10Output: (no output)

# Create annotated tag with message
git tag -a v1.1.0 -m Release version 11Output: (no output)

# List all tags
git tag
# Output: v1.0.0#         v1.1.0

# Checkout specific tag
git checkout v1.00ut: Note: checking out 'v10...
#         You are in 'detached HEAD' state...

# Go back to main branch
git checkout main
```

### 8. Branch Management with Naming Convention
```bash
# Create feature branch following convention
git checkout -b feature/user-authentication/ISSUE-123 Make changes
echo "// User authentication logic" > auth.js
git add auth.js
git commit -m "feat: implement user authentication

- Add login functionality
- Add session management
- Fixes ISSUE-123

# Create bugfix branch
git checkout -b bugfix/login-error/ISSUE-124# Fix the bug
echo "// Fixed login error" >> auth.js
git add auth.js
git commit -m "fix: resolve login error

- Fix null pointer exception
- Add error handling
- Fixes ISSUE-124"

# List all branches
git branch
# Output:   bugfix/login-error/ISSUE-124
#         * feature/user-authentication/ISSUE-123
#           main
#           stable
```

### 9. Merging and Conflict Resolution
```bash
# Switch to main and merge feature branch
git checkout main
git merge feature/user-authentication/ISSUE-123Output: Merge made by the 'recursive' strategy.
#         auth.js | 1 +
#        1anged,1nsertion(+)

# Try to merge bugfix branch (might cause conflict)
git merge bugfix/login-error/ISSUE-124# Output: Auto-merging auth.js
#         CONFLICT (content): Merge conflict in auth.js
#         Automatic merge failed; fix conflicts and then commit the result.

# Check status during conflict
git status
# Output: You have unmerged paths.
#         (fix conflicts and run "git commit")
#         (use git merge --abort" to abort the merge)
#         
#         Unmerged paths:
#           (use "git add <file>..." to mark resolution)
#                 both modified:   auth.js

# Abort merge to start over
git merge --abort
# Output: (no output)
```

### 10. Reset Operations
```bash
# View commit history
git log --oneline
# Output: abc1234at: implement user authentication
#         def5678 feat: add application logic
#         ghi9012re: add .gitignore file
#         jkl3456t: initial project setup with basic files

# Soft reset (keeps changes in staging area)
git reset --soft HEAD~1
# Output: (no output)

# Check status
git status
# Output: Changes to be committed:
#           (usegit restore --staged <file>..." to unstage)
#                 modified:   auth.js

# Mixed reset (keeps changes in working directory)
git reset --mixed HEAD~1
# Output: Unstaged changes after reset:
#         M       auth.js

# Hard reset (discards all changes)
git reset --hard HEAD~1
# Output: HEAD is now at def5678 feat: add application logic
```

### 11. Using Reflog and Amending Commits
```bash
# View reflog to see all Git operations
git reflog
# Output: def5678{0}: reset: moving to HEAD~1
#         abc1234{1}: merge feature/user-authentication/ISSUE-123 Merge made by the 'recursive' strategy.
#         def5678 HEAD@{2}: checkout: moving from feature/user-authentication/ISSUE-123 to main
#         ...

# Make a commit
echo "//New feature" > new-feature.js
git add new-feature.js
git commit -m "feat: add new feature"

# Amend the commit to add more files
echo "// Documentation" > docs.md
git add docs.md
git commit --amend -m "feat: add new feature with documentation
# Output: [main 1234567t: add new feature with documentation
#         2 changed,2tions(+)
#         create mode 100644 docs.md
#         create mode 100644w-feature.js
```

### 12. Visualizing Commit History
```bash
# View all branches in log
git log --all --graph --oneline --decorate
# Output: * 1234567HEAD -> main) feat: add new feature with documentation
#         * abc1234at: implement user authentication
#         * def5678 feat: add application logic
#         * ghi9012re: add .gitignore file
#         * jkl3456t: initial project setup with basic files

# View log with more details
git log --pretty=format:%h - %an, %ar : %s
# Output: 1234567Your Name, 2 hours ago : feat: add new feature with documentation
#         abc1234Your Name, 3 hours ago : feat: implement user authentication
#         def5678Your Name, 4 hours ago : feat: add application logic
```

### 13. Garbage Collection
```bash
# Git automatically runs garbage collection, but you can force it
git gc
# Output: Enumerating objects: 15#         Counting objects: 100% (15/15), done.
#         Delta compression using up to 8 threads
#         Compressing objects: 100% (10/10), done.
#         Writing objects: 100% (15/15), done.
#         Total 15 (delta 2), reused 0 (delta0 pack-reused 15)

# Clean up unreferenced objects
git prune
# Output: (no output if nothing to prune)
```

### Important Notes:
- **Commit Immutability**: Once a commit is created, it cannot be modified or deleted directly. Only the garbage collector can remove orphaned commits.
- **Version Numbers**: Follow semantic versioning (MAJOR.MINOR.PATCH) for releases
- **Conventional Commits**: Use format `type(scope): description` (e.g., `feat(auth): add login functionality`)
- **Branch Naming**: Use format `<type>/<name>/<issue-id>` for organized development 