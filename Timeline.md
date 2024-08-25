# Git Commit Date, Author Date, Name, and Email Modification Guide

This document provides instructions for modifying commit details in Git, including commit date, author date, author name, and author email.

## Modifying Author Date

To change the author date of the most recent commit:

```bash
git commit --amend --date="author-date" --no-edit
```

### Example:
- Set the author date to August 12, 2012, at 20:00:00:
  ```bash
  git commit --amend --date="2012-08-12T20:00:00" --no-edit
  ```

## Modifying Author Name and Email

To change the author name and email of the most recent commit:

```bash
git commit --amend --author="New Name <new.email@example.com>" --no-edit
```

### Example:
- Set the author to "anonymous" with the email "anonymous@gmail.com":
  ```bash
  git commit --amend --author="anonymous <anonymous@gmail.com>" --no-edit
  ```

## Modifying Commit Date and Details in Amended Commits

To change the committer date, name, and email:

```bash
GIT_COMMITTER_DATE="committer-date" git commit --amend --no-edit
```

To also change the committer's name and email:

```bash
GIT_COMMITTER_NAME="New Name" GIT_COMMITTER_EMAIL="new.email@example.com" git commit --amend --no-edit
```

### Example:
- Set the committer date to August 12, 2012, at 20:00:00, with the name "anonymous" and email "anonymous@gmail.com":
  ```bash
  GIT_COMMITTER_DATE="2012-08-12T20:00:00" GIT_COMMITTER_NAME="anonymous" GIT_COMMITTER_EMAIL="anonymous@gmail.com" git commit --amend --no-edit
  ```

## Rewriting History for Specific Commits

To modify the author and committer details of specific commits, you can use `git filter-branch` with an environment filter. This is useful for rewriting historical commits.

### Example:
To change the author and committer details for a specific commit:

```bash
git filter-branch --env-filter '
    if [ "$GIT_COMMIT" = "2235df57ed3f2bc8ddee8a3e1cf4f3cb3b50b59f" ]; then
        export GIT_AUTHOR_DATE="1990-01-01T10:00:00"
        export GIT_COMMITTER_DATE="1995-01-01T10:00:00"
        export GIT_COMMITTER_NAME="aa"
        export GIT_COMMITTER_EMAIL="aa@gmail.com"
        export GIT_AUTHOR_NAME="bb"
        export GIT_AUTHOR_EMAIL="bb@gmail.com"
    fi
' --tag-name-filter cat -- --branches --tags
```

**Note**: Rewriting history can affect other collaborators' work. Use it with caution and ensure all team members are aware of the changes.

## Conclusion

Modifying commit details in Git allows for correction of errors or adjustments to historical data. Always double-check the commit hash and dates to avoid unintended changes, especially when rewriting history.
