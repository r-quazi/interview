##  Devops Interview questions | Devops Telephonic interview - 5 ( Mock Interview ) 
https://www.youtube.com/watch?v=bswufdMDAMM&list=PLLYW3zEOaqlLShAk9pd4FQ34KOpY7EJAq&index=5

-------------------------

1. What is .git directory and what it contains ?
Ans :

The `.git` directory is a core component of a Git repository. It is a hidden directory located at the root of a Git project, and it stores all the information and metadata about the repository's history, configuration, and the state of the project.

Here's a breakdown of what the `.git` directory typically contains:

1. **Objects**: This directory contains the actual data for all the objects in the repository, such as commits, trees, and blobs. Git uses a content-addressable file system, and this is where the content of your project is stored in a compressed format.

2. **refs**: This directory stores references to commits. Branches, tags, and other references are stored here. Each reference is represented by a file in this directory. For example, `refs/heads/master` points to the latest commit in the `master` branch.

3. **HEAD**: This file points to the currently checked-out branch or commit. It's essentially a symbolic reference to the currently active branch.

4. **config**: This file contains configuration settings for the repository. These settings can include user information, remote repository URLs, and other configuration options.

5. **description**: A simple text file that can be used for a description of the repository. It is typically displayed by some Git hosting services.

6. **hooks**: This directory contains scripts that can be executed at various points in the Git workflow, such as pre-commit and post-receive hooks. These scripts allow you to customize and automate actions in your Git workflow.

7. **index**: This file is the Git index, also known as the staging area. It keeps track of changes you have made but haven't yet committed. It stores references to files and their associated states (e.g., added, modified, deleted).

8. **logs**: This directory contains log files, including reflogs. Reflogs keep a record of when branches were updated or references were modified. They can be useful for recovering lost commits.

9. **info**: This directory contains auxiliary information about the repository, such as exclude patterns for ignored files.

10. **hooks**: This directory can contain custom scripts that Git executes at specific points in the version control process. These scripts allow you to automate tasks or enforce rules in your Git workflow.

11. **modules**: If the repository uses Git submodules, information about those submodules is stored here.

12. **config**: This file contains repository-specific configuration settings. It includes information like the remote repository URLs and user information for commits.

13. **packed-refs**: This file is a text file containing packed references, which are a more efficient way to store references in a large repository.

14. **ORIG_HEAD**: This file is created by Git during certain operations like resetting branches. It keeps a reference to the previous state of the HEAD.

It's important to note that while the `.git` directory contains all the essential information about the repository, it's typically hidden from casual users to prevent accidental modification, as altering the contents of this directory can lead to data loss or corruption in your Git repository. Most Git commands and tools interact with the `.git` directory on your behalf, so you don't usually need to access or modify it directly.

NO VOICE -----------------
