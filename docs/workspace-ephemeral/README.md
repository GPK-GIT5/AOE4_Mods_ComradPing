# Workspace Ephemeral Folders

The `.tmp/` and `Temporary/` folders from the private workspace are not present in this public repository.

## Purpose

In the private workspace, these are scratch directories for transient pipeline outputs and in-progress staging work. Neither has enforced structure and neither is version-controlled.

| Folder | Use |
|---|---|
| `.tmp/` | Short-lived pipeline outputs and intermediate extraction files |
| `Temporary/` | Manual staging area for in-progress experiments |

## Why excluded

Contents are transient working state with no persistent value. Both are listed in `.gitignore`.

## Integration points

None. Neither folder is referenced by any script, workflow, or mod source.
