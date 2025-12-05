# Exercise 3 - Release Management: Tags, Cherry-Picks & Patch Versions

## Description
This exercise introduces how to create version tags, publish releases, cherry-pick commits into release branches, and publish patch versions. These are essential when release and applying fixes without merging all development changes into production.

## Prerequisite
Before starting this exercise, ensure you have:
- Git installed on your machine and access rights to publish GitHub releases
- A repository with a main branch containing completed features
- At least one commit in main that can be tagged for release
- Another commit that will be cherry-picked to create a patch version

## Use Cases
- Creating stable releases for deployment
- Applying hotfixes using cherry-pick
- Maintaining clean version history with semantic versioning (v1.0.0, v1.0.1, etc.)
- Documenting changes through GitHub release notes

## Exercise Details
### 1. Tag and Release a Package
Create an official release version using Git tags and GitHub Releases.

**Steps:**
- Ensure your local main branch is up to date
```
git checkout main
git pull origin main
```

- Create a tag for the release (example version: v1.0.0)
```
git tag v1.0.0
git push origin v1.0.0
```

- On GitHub, navigate to Releases → Create a new release

![ex3_tag_1.png](images/ex3_tag_1.png)
![ex3_tag_2.png](images/ex3_tag_2.png)
![ex3_tag_3.png](images/ex3_tag_3.png)

- Choose the tag v1.0.0 (or create it from the UI)
- Add a release title and description
- Publish the release/ Save 

![ex3_release_1.png](images/ex3_release_1.png)

### 2. Cherry-Pick a Commit to a Release Branch
Apply a specific fix to an existing release branch without merging all new development.

**Conditions**
- A commit exists on main (or another branch) that should be included in the patch release.
- A release branch already exists, e.g. release/v1.0.0

**Steps:**
- Create a release branch based on the `v1.0.0` tag
```
git checkout main
git pull origin main
git checkout -b release/v1.0.0 v1.0.0
git push origin release/v1.0.0
```

- Make a new commit on main simulating a bug fix (eg: update a file)

```
git checkout -b hotfix/add-missing-file
echo "Hotfix content" >> hotfix.txt
git add hotfix.txt
git commit -m "hotfix: add hotfix file"
git push origin hotfix/add-missing-file
```

Get this commit hash using
```
git log --oneline
```
![ex3_cherrypick_1.png](images/ex3_cherrypick_1.png)


- Checkout the release branch
```
git checkout release/v1.0.0
git pull origin release/v1.0.0
```

- Cherry-pick the desired commit (Your commit hash will be different according to git log --oneline above)
```
git cherry-pick <commit-hash>
git cherry-pick 5a8d7d4
```

- If conflicts occur, resolve them then continue
```
git add <file>
git cherry-pick --continue
```

- Push the updated release branch:
```
git push origin release/v1.0
```

### 3. Create a Patch Release

Publish a new version (e.g., v1.0.1) containing only the cherry-picked fix.

**Steps:**
- Go to Releases → Draft a new release
- Create a new tag for the patch: `v1.0.1`
- Select the target branch: `release/v1.0.0`
- Add release notes describing the fix and the cherry-picked commit
- Publish the patch release

![ex3_patch_release_1.png](images/ex3_patch_release_1.png)
![ex3_patch_release_2.png](images/ex3_patch_release_2.png)

## Expected Output
- A Git tag (v1.0.0) created and pushed successfully
- A published release on GitHub for version v1.0.0
- A commit successfully cherry-picked into the release branch
- A patch release (v1.0.1) created and published