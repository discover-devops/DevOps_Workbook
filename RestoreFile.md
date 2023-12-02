
To restore the previous version of a file in Git, you can use the `git checkout` command. 
Here's a step-by-step guide:

### 1. Identify the Commit Hash or Branch

First, you need to identify the commit hash or branch that contains the version of the file you want to restore. You can use `git log` to view the commit history and find the specific commit hash.

```bash
git log
```

### 2. Use `git checkout` to Restore the File

Once you have identified the commit hash (or branch name), use the following command to restore the file:

```bash
git checkout <commit_hash> -- <file_path>
```

Replace `<commit_hash>` with the actual commit hash and `<file_path>` with the path to the file you want to restore. For example:

```bash
git checkout abc1234 -- path/to/your/file.txt
```

This command will restore the file to the state it was in at the specified commit. Note that this will only modify the working directory and the local copy of the file. If you want to commit this change and make it permanent, you need to create a new commit.

### 3. (Optional) Commit the Changes

After restoring the file, you may want to commit the changes to make them permanent in your version history. Use the following commands to stage and commit the changes:

```bash
git add <file_path>
git commit -m "Restore <file_path> to a previous version"
```

Replace `<file_path>` with the actual path to the file you restored.

### Important Note:

If you are using Git version 2.23 or later, it's recommended to use the `git restore` command, which provides a clearer syntax for this operation:

```bash
git restore --source=<commit_hash> --staged --worktree -- <file_path>
```

This command achieves the same result as the `git checkout` command.

Remember to replace `<commit_hash>` and `<file_path>` with the appropriate values for your situation.
