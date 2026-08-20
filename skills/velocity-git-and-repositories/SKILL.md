---
name: velocity-git-and-repositories
description: Git version control rules, repository URL normalization, branch management, and safety boundaries for Velocity workspaces.
---

# Velocity Git & Repositories Skill

This skill defines rules and procedures for managing Git repositories inside Velocity Cloud Sandboxes.

## Repository Parameter Format & Normalization
When calling create_workspace, pass standard repository formats:
- **Blank-workspace**: Creates an empty container with no initial repository cloned.
- **GitHub / GitLab URL**: github.com/username/repository or gitlab.com/username/repository.
- Protocol prefixes (https://, git@) are automatically normalized.

## Agent Safety Boundaries

> [!CAUTION]
> **CRITICAL AGENT SAFETY RULE**:
> Never run git commit, git push, or alter remote repository branches unless the user has explicitly commanded you to commit or push changes.

## Git Operations Protocol inside Workspace

1. **Inspection**: Run git status and git diff to review active workspace changes.
2. **Branching**: Create feature branches (git checkout -b feature/name) before modifying project code.
3. **Private Repositories**: When cloning private repositories inside the container, request user SSH keys or GitHub Personal Access Tokens (PAT). Never hardcode credentials into scripts or activity logs.
