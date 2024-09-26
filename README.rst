git-sweep-latest
================

`datopic-git-sweep-latest 0.1.1 <https://pypi.org/project/datopic-git-sweep-latest/0.1.1/#description>`_

Introduction
------------

`git-sweep` is a tool designed to help clean up stale, merged branches from a Git repository. As development progresses, many feature branches get merged into the main branch (e.g., master, main, dev) and remain in the repository even though they are no longer needed. Over time, this can lead to clutter, making it harder to manage your repository. `git-sweep` automates the cleanup process by identifying and removing branches that have already been merged, helping to keep your repository clean and organized.

Why Use git-sweep?
------------------

In collaborative environments, multiple feature branches are regularly created and merged. Without proper cleanup, the number of stale branches grows. Here are some common reasons to use `git-sweep`:

- **Avoid Repository Clutter**: Old merged branches make it hard to find relevant branches and manage active development.
- **Improve Team Collaboration**: A clean repository helps developers focus on relevant branches.
- **Better Performance**: Fewer branches lead to faster repository performance, especially with remote operations.
- **Prevent Mistakes**: Old branches may lead to accidental checkouts. Cleanup reduces the chance of confusion.

Benefits of git-sweep
---------------------

- **Automates Branch Cleanup**: Automatically identify and delete old branches, saving time and effort.
- **Customizable Workflow**: You can specify the remote repository and branch (e.g., master, dev, main) to check for merges and skip specific branches if needed.
- **Safe Deletion Process**: A preview mode allows you to review the branches before deletion.
- **Supports Remote Cleanup**: Branches are deleted from both local and remote repositories.
- **Simplifies Maintenance**: Regular cleanups improve the overall health of your repository.

How to Use git-sweep
--------------------

### 1. Installation

Install `git-sweep` using pip:

.. code:: bash

    pip install datopic-git-sweep-latest==0.1.1

### 2. Navigate to Your Repository

Navigate to the Git repository you wish to clean:

.. code:: bash

    cd /path/to/your/repository

### 3. Preview Merged Branches

To preview branches that are safe to delete, specify the primary branch using the `--master` flag:

.. code:: bash

    git-sweep preview --master dev_puru

This will:

- Fetch the latest info from the remote repository.
- List all branches merged into `dev_puru` (or whichever branch is specified).
- Display a preview without making changes.

### 4. Clean Up Merged Branches

Once you're satisfied with the preview, you can delete the merged branches:

.. code:: bash

    git-sweep cleanup --master dev_puru

To force deletion without confirmation, use the `--force` flag:

.. code:: bash

    git-sweep cleanup --master dev_puru --force

### 5. Skipping Specific Branches

To skip specific branches during cleanup, use the `--skip` flag:

.. code:: bash

    git-sweep cleanup --master dev_puru --skip main,master

### 6. Manual Deletion (Optional)

If `git-sweep` fails to delete certain branches, you can manually delete them:

.. code:: bash

    git push origin --delete branch-name

Example Workflow
----------------

For a repository with the following setup:

- Primary branch: `dev_puru`
- Merged branches: `feature/add-login`, `feature/add-signup`, `bugfix/typo-fix`

Step 1: Preview merged branches:

.. code:: bash

    git-sweep preview --master dev_puru

Step 2: Clean up merged branches:

.. code:: bash

    git-sweep cleanup --master dev_puru

Step 3: Skip specific branches:

.. code:: bash

    git-sweep cleanup --master dev_puru --skip main

Error Handling
--------------

### Error: Failed to Delete Branches

If you encounter the following error:

.. code:: bash

    error: failed to push some refs to 'https://github.com/purusharma168/git-sweep-latest.git'

### Step-by-Step Resolution

1. **Check for Branch Protection Rules**:

   Branch protection rules on GitHub can prevent deletion of branches like `main` or `master`. To modify these rules:

   - Go to the repository on GitHub.
   - Click on the "Settings" tab.
   - Under "Branches", modify the rules under "Branch Protection Rules".

2. **Ensure Correct Permissions**:

   Ensure that your Personal Access Token (PAT) has the `repo` scope, which includes branch deletion permissions. If needed, generate a new token with the correct scopes:

.. code:: bash

    git remote set-url origin https://<your-new-token>@github.com/username/git-sweep-latest.git
