## Types of Git Tags

1. **Lightweight Tags**
   - Simple pointers to specific commits
   - Contains only commit information
   - Created without additional metadata
   ```bash
   git tag v1.0.0
   ```

2. **Annotated Tags**
   - Stored as full objects in the Git database
   - Contains extra metadata like:
     - Tagger name
     - Email
     - Date
     - Tagging message
   ```bash
   git tag -a v1.0.0 -m "Release version 1.0.0"
   ```

## Common Git Tag Commands

### Creating Tags

```bash
# Create lightweight tag
git tag v1.0.0

# Create annotated tag
git tag -a v1.0.0 -m "Release version 1.0.0"

# Tag a specific commit
git tag -a v1.0.0 9fceb02 -m "Tag message"
```

### Listing Tags

```bash
# List all tags
git tag

# List tags matching a pattern
git tag -l "v1.8.5*"

# Show tag details
git show v1.0.0
```

### Pushing Tags

```bash
# Push a specific tag
git push origin v1.0.0

# Push all tags
git push origin --tags
```

### Deleting Tags

```bash
# Delete local tag
git tag -d v1.0.0

# Delete remote tag
git push origin --delete v1.0.0
```

### Checking Out Tags

```bash
# View the state of the repository at tag
git checkout v1.0.0

# Create a new branch from tag
git checkout -b branch_name v1.0.0
```

## Best Practices

1. **Use Semantic Versioning**
   - Follow the MAJOR.MINOR.PATCH format
   - Example: v1.2.3
   - Makes version management more systematic

2. **Always Use Annotated Tags for Releases**
   - Provides more information about the release
   - Helps maintain project history
   - Includes tagger information and date

3. **Tag Naming Conventions**
   - Use consistent prefix (v1.0.0 vs 1.0.0)
   - Be consistent with capitalization
   - Consider including additional identifiers for different types of releases
     - v1.0.0-beta
     - v1.0.0-rc1

4. **Tag Description Guidelines**
   - Include clear, concise descriptions
   - List major changes or features
   - Reference relevant issue numbers or pull requests

## Common Workflows

### Release Workflow
1. Finish and test all changes
2. Update version numbers in project files
3. Create an annotated tag
4. Push the tag to remote
```bash
git tag -a v1.0.0 -m "Release 1.0.0: [List major changes]"
git push origin v1.0.0
```

### Hotfix Workflow
1. Create branch from tag
2. Make fixes
3. Create new patch version tag
```bash
git checkout -b hotfix_branch v1.0.0
# Make fixes
git tag -a v1.0.1 -m "Hotfix: [Description]"
```

## Troubleshooting

### Common Issues and Solutions

1. **Tag Already Exists**
   ```bash
   # Force update an existing tag
   git tag -fa v1.0.0 -m "Updated tag message"
   git push origin --force v1.0.0
   ```

2. **Wrong Tag Created**
   ```bash
   # Delete wrong tag and create new one
   git tag -d wrong_tag
   git push origin --delete wrong_tag
   git tag -a correct_tag -m "Correct tag message"
   ```

3. **Missing Tags After Clone**
   ```bash
   # Fetch all tags
   git fetch --tags
   ```

# Example Workflow

1. Start new feature from prod:
```bash
git checkout prod
git pull                       # ensure prod is up to date
git checkout -b feature/login  # create feature branch
# Make your changes
git commit -m "Add login feature"
```

2. Create release branch:
```bash
git checkout prod              # go back to prod
git pull                       # ensure up to date
git checkout -b release/v1.1.0 # create release branch
```

3. Merge feature into release (direct merge):
```bash
git checkout release/v1.1.0
git merge feature/login
# Test everything in release branch
# Fix any issues directly in release if needed
git push origin release/v1.1.0
```

4. Create and merge PR:
```bash
# Go to GitHub
# Create PR: release/v1.1.0 → prod
# Review code
# Merge PR into prod
```

5. Create tag after PR is merged:
```bash
git checkout prod
git pull                       # get the merged changes
git tag -a v1.1.0 -m "Release version 1.1.0"
git push origin v1.1.0
```

6. Clean up (optional):
```bash
git branch -d feature/login    # delete local feature branch
git branch -d release/v1.1.0   # delete local release branch
git push origin --delete feature/login    # delete remote feature branch
git push origin --delete release/v1.1.0   # delete remote release branch
```

release_{env_branch}_{feature_name}