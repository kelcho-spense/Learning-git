# Advanced Git Operations

Have you gotten accustomed to the basics of `git`, but the advanced concepts make you  *scratch your head* ?

![hard-things](scratch-head.webp)

### Feature Branch workflow

The core idea behind the Feature Branch Workflow is that all feature development should take place in a dedicated branch instead of the `main` branch. This encapsulation makes it easy for multiple developers to work on a particular feature without disturbing the main codebase. It also means the `main` branch will never contain broken code, which is a huge advantage for continuous integration environments.

#### Start with the main branch

All feature branches are created off the latest code state of a project. This guide assumes this is maintained and updated in the `main` branch.

```css
git checkout main
git fetch origin 
git reset --hard origin/main
```

#### Create the repository

This switches the repo to the `main` branch, pulls the latest commits and resets the repo's local copy of `main` to match the latest version.

#### Create a new-branch

Use a separate branch for each feature or issue you work on. After creating a branch, check it out locally so that any changes you make will be on that branch.

```css
git checkout -b new-feature
```

This checks out a branch called new-feature based on `main`, and the -b flag tells Git to create the branch if it doesn’t already exist.

#### Update, add, commit, and push changes

On this branch, edit, stage, and commit changes in the usual fashion, building up the feature with as many commits as necessary. Work on the feature and make commits like you would any time you use Git. When ready, push your commits, updating the feature branch on Bitbucket.

```xml
git status
git add <some-file>
git commit
```

#### Push feature branch to remote

It’s a good idea to push the feature branch up to the central repository. This serves as a convenient backup, when collaborating with other developers, this would give them access to view commits to the new branch.

```js
git push -u origin new-feature
```

This command pushes new-feature to the central repository (origin), and the -u flag adds it as a remote tracking branch. After setting up the tracking branch, `git push` can be invoked without any parameters to automatically push the new-feature branch to the central repository. To get feedback on the new feature branch, create a pull request in a repository management solution like bitbucket cloud or GitHub. From there, you can add reviewers and make sure everything is good to go before merging.

#### Resolve feedback

Now teammates comment and approve the pushed commits. Resolve their comments locally, commit, and push the suggested changes to Bitbucket. Your updates appear in the pull request.

#### Merge your pull request

Before you merge, you may have to resolve merge conflicts if others have made changes to the repo. When your pull request is approved and conflict-free, you can add your code to the `main` branch. Merge from the pull request in Bitbucket.

#### Pull requests

Once a pull request is accepted, the actual act of publishing a feature is much the same as in the Centralized Workflow. First, you need to make sure your local `main` is synchronized with the upstream `main`. Then, you merge the feature branch into `main` and push the updated `main` back to the central repository.

Pull requests can be facilitated by source code management solutions like Bitbucket Cloud.

#### Example feature branching workflow

---

The following is an example of the type of scenario in which a feature branching workflow is used. The scenario is that of a team doing code review around on a new feature pull request. This is one example of the many purposes this model can be used for.

#### Mary begins a new feature

![Feature branch illustration](https://wac-cdn.atlassian.com/dam/jcr:223f5106-2191-4450-8916-e5c80d7d907a/02.svg?cdnVersion=2688)

Before she starts developing a feature, Mary needs an isolated branch to work on. She can request a new branch with the following command:

```css
git checkout -b marys-feature main
```

This checks out a branch called `marys-feature` based on `main,` and the -b flag tells Git to create the branch if it doesn’t already exist. On this branch, Mary edits, stages, and commits changes in the usual fashion, building up her feature with as many commits as necessary:

```xml
git status
git add <some-file>
git commit
```

#### Mary goes to lunch

![Push to central repository](https://wac-cdn.atlassian.com/dam/jcr:e2c88c1b-fb28-46a3-93be-c1c45f86bd1c/03%20(1).svg?cdnVersion=2688)

Mary adds a few commits to her feature over the course of the morning. Before she leaves for lunch, it’s a good idea to push her feature branch up to the central repository. This serves as a convenient backup, but if Mary was collaborating with other developers, this would also give them access to her initial commits.

```bash
git push -u origin marys-feature
```

This command pushes `marys-feature` to the central repository (origin), and the -u flag adds it as a remote tracking branch. After setting up the tracking branch, Mary can call `git push` without any parameters to push her feature.

#### Mary finishes her feature

![Pull request](https://wac-cdn.atlassian.com/dam/jcr:d0c471b4-61c8-4005-86bc-904d894e391b/04.svg?cdnVersion=2688)

When Mary gets back from lunch, she completes her feature. Before merging it into `main`, she needs to file a pull request letting the rest of the team know she's done. But first, she should make sure the central repository has her most recent commits:

```bash
git push
```

Then, she files the pull request in her Git GUI asking to merge `marys-feature` into `main`, and team members will be notified automatically. The great thing about pull requests is that they show comments right next to their related commits, so it's easy to ask questions about specific changesets.

#### Bill receives the pull request

![Review pull request illustration](https://wac-cdn.atlassian.com/dam/jcr:2119c2a3-7dff-43ad-bf98-77672d93242f/05%20(1).svg?cdnVersion=2688)

Bill gets the pull request and takes a look at `marys-feature.` He decides he wants to make a few changes before integrating it into the official project, and he and Mary have some back-and-forth via the pull request.

#### Mary makes the changes

![Pull request revisions](https://wac-cdn.atlassian.com/dam/jcr:1c466900-dffa-4912-8764-79943755dbf9/06%20(1).svg?cdnVersion=2688)

To make the changes, Mary uses the exact same process as she did to create the first iteration of her feature. She edits, stages, commits, and pushes updates to the central repository. All her activity shows up in the pull request, and Bill can still make comments along the way.

If he wanted, Bill could pull `marys-feature` into his local repository and work on it on his own. Any commits he added would also show up in the pull request.

#### Mary publishes her feature

![Publishing feature](https://wac-cdn.atlassian.com/dam/jcr:09308632-38a3-4637-bba2-af2110629d56/07.svg?cdnVersion=2688)

Once Bill is ready to accept the pull request, someone needs to merge the feature into the stable project (this can be done by either Bill or Mary):

```css
git checkout main
git pull
git pull origin marys-feature
git push
```

This process often results in a merge commit. Some developers like this because it’s like a symbolic joining of the feature with the rest of the code base. But, if you’re partial to a linear history, it’s possible to rebase the feature onto the tip of `main` before executing the merge, resulting in a fast-forward merge.

Some GUI’s will automate the pull request acceptance process by running all of these commands just by clicking an “Accept” button. If yours doesn’t, it should at least be able to automatically close the pull request when the feature branch gets merged into `main.`

Meanwhile, John is doing the exact same thing.

While Mary and Bill are working on marys-feature and discussing it in her pull request, John is doing the exact same thing with his own feature branch. By isolating features into separate branches, everybody can work independently, yet it’s still trivial to share changes with other developers when necessary.

---

### Gitflow workflow

![1746388779271](1746388779271.png)

Gitflow is an alternative Git branching model that involves the use of feature branches and multiple primary branches. It was first published and made popular by Vincent Driessen at nvie. Compared to trunk-based development, Gitflow has numerous, longer-lived branches and larger commits

##### How it works {id="how-it-works_1"}

![Git workflow](https://wac-cdn.atlassian.com/dam/jcr:a13c18d6-94f3-4fc4-84fb-2b8f1b2fd339/01%20How%20it%20works.svg?cdnVersion=2688)

##### Develop and main branches

Instead of a single `main` branch, this workflow uses two branches to record the history of the project. The `main` branch stores the official release history, and the `develop` branch serves as an integration branch for features. It's also convenient to tag all commits in the `main` branch with a version number.

The first step is to complement the default `main` with a `develop` branch. A simple way to do this is for one developer to create an empty `develop` branch locally and push it to the server:

```bash
git branch develop
git push -u origin develop
```

This branch will contain the complete history of the project, whereas `main` will contain an abridged version. Other developers should now clone the central repository and create a tracking branch for `develop.`

When using the git-flow extension library, executing `git flow init` on an existing repo will create the `develop` branch:

```js
$ git flow init


Initialized empty Git repository in ~/project/.git/
No branches exist yet. Base branches must be created now.
Branch name for production releases: [main]
Branch name for "next release" development: [develop]


How to name your supporting branch prefixes?
Feature branches? [feature/]
Release branches? [release/]
Hotfix branches? [hotfix/]
Support branches? [support/]
Version tag prefix? []


$ git branch
* develop
 main
```

##### Feature branches

---

###### Step 1. Create the repository

Each new feature should reside in its own branch, which can be [pushed to the central repository](https://www.atlassian.com/git/tutorials/syncing/git-push) for backup/collaboration. But, instead of branching off of `main`, `feature` branches use `develop` as their parent branch. When a feature is complete, it gets [merged back into develop](https://www.atlassian.com/git/tutorials/using-branches/git-merge). Features should never interact directly with `main`.

![Git workflow - feature branches](https://wac-cdn.atlassian.com/dam/jcr:34c86360-8dea-4be4-92f7-6597d4d5bfae/02%20Feature%20branches.svg?cdnVersion=2688)

Note that `feature` branches combined with the `develop` branch is, for all intents and purposes, the Feature Branch Workflow. But, the Gitflow workflow doesn’t stop there.

`Feature` branches are generally created off to the latest `develop` branch.

###### Creating a feature branch

Without the git-flow extensions:

```css
git checkout develop
git checkout -b feature_branch
```

When using the git-flow extension:

```css
git flow feature start feature_branch
```

Continue your work and use Git like you normally would.

###### Finishing a feature branch

When you’re done with the development work on the feature, the next step is to merge the `feature_branch` into `develop`.

Without the git-flow extensions:

```bash
git checkout develop
git merge feature_branch
```

Using the git-flow extensions:

```css
git flow feature finish feature_branch
```

##### Release branches

---

![Git workflow - release branches](https://wac-cdn.atlassian.com/dam/jcr:8f00f1a4-ef2d-498a-a2c6-8020bb97902f/03%20Release%20branches.svg?cdnVersion=2688)

Once `develop` has acquired enough features for a release (or a predetermined release date is approaching), you fork a `release` branch off of `develop`. Creating this branch starts the next release cycle, so no new features can be added after this point—only bug fixes, documentation generation, and other release-oriented tasks should go in this branch. Once it's ready to ship, the `release` branch gets merged into `main` and tagged with a version number. In addition, it should be merged back into `develop`, which may have progressed since the release was initiated.

Using a dedicated branch to prepare releases makes it possible for one team to polish the current release while another team continues working on features for the next release. It also creates well-defined phases of development (e.g., it's easy to say, “This week we're preparing for version 4.0,” and to actually see it in the structure of the repository).

Making `release` branches is another straightforward branching operation. Like `feature` branches, `release` branches are based on the `develop` branch. A new `release` branch can be created using the following methods.

Without the git-flow extensions:

```css
git checkout develop
git checkout -b release/0.1.0
```

When using the git-flow extensions:

```js
$ git flow release start 0.1.0
Switched to a new branch 'release/0.1.0'
```

Once the release is ready to ship, it will get merged it into `main` and `develop`, then the `release` branch will be deleted. It’s important to merge back into `develop` because critical updates may have been added to the `release` branch and they need to be accessible to new features. If your organization stresses code review, this would be an ideal place for a pull request.

To finish a `release` branch, use the following methods:

Without the git-flow extensions:

```css
git checkout main
git merge release/0.1.0
```

Or with the git-flow extension:

```bash
git flow release finish '0.1.0'
```

##### Hotfix branches

---

![Hotfix branch within git workflow](https://wac-cdn.atlassian.com/dam/jcr:cc0b526e-adb7-4d45-874e-9bcea9898b4a/04%20Hotfix%20branches.svg?cdnVersion=2688)

Maintenance or `“hotfix”` branches are used to quickly patch production releases. `Hotfix` branches are a lot like `release` branches and `feature` branches except they're based on `main` instead of `develop`. This is the only branch that should fork directly off of `main`. As soon as the fix is complete, it should be merged into both `main` and `develop` (or the current `release` branch), and `main` should be tagged with an updated version number.

Having a dedicated line of development for bug fixes lets your team address issues without interrupting the rest of the workflow or waiting for the next release cycle. You can think of maintenance branches as ad hoc `release` branches that work directly with `main`. A `hotfix` branch can be created using the following methods:

Without the git-flow extensions:

```css
git checkout main
git checkout -b hotfix_branch
```

When using the git-flow extensions:

```scss
$ git flow hotfix start hotfix_branch
```

Similar to finishing a `release` branch, a `hotfix` branch gets merged into both `main` and `develop.`

```css
git checkout main
git merge hotfix_branch
git checkout develop
git merge hotfix_branch
git branch -D hotfix_branch
```

```scss
$ git flow hotfix finish hotfix_branch
```

### Forking workflow

The Forking Workflow is fundamentally different than other popular Git workflows. Instead of using a single server-side repository to act as the “central” codebase, it gives every developer their own server-side repository. This means that each contributor has not one, but two Git repositories: a private local one and a public server-side one. The Forking Workflow is most often seen in public open source projects.

#### How it works

1. A developer 'forks' an 'official' server-side repository. This creates their own server-side copy.
2. The new server-side copy is cloned to their local system.
3. A Git remote path for the 'official' repository is added to the local clone.
4. A new local feature branch is created.
5. The developer makes changes on the new branch.
6. New commits are created for the changes.
7. The branch gets pushed to the developer's own server-side copy.
8. The developer opens a pull request from the new branch to the 'official' repository.
9. The pull request gets approved for merge and is merged into the original server-side repository

To integrate the feature into the official codebase, the maintainer pulls the contributor’s changes into their local repository, checks to make sure it doesn’t break the project, merges it into their local `main` branch, then pushes the `main` branch to the official repository on the server. The contribution is now part of the project, and other developers should pull from the official repository to synchronize their local repositories.

#### Forking vs cloning

It's important to note that "forked" repositories and "forking" are not special operations. Forked repositories are created using the standard git clone command. Forked repositories are generally "server-side clones" and usually managed and hosted by a 3rd party Git service like Bitbucket. There is no unique Git command to create forked repositories. A clone operation is essentially a copy of a repository and its history.

### Git Rebasing

![1746390511127](1746390511127.png)

Git Rebase is a command used to move or combine a sequence of commits to a new base commit

#### Types of Git Rebase

##### ****1. Interactive Rebase (git rebase -i)****

* This allows you to edit, squash, reorder, or delete commits in your branch. It gives you full control over the commit history, making it useful for cleaning up commit messages or combining multiple commits into one.
* It squashing commits to combine them into a single commit.
* Git rebase reordering commits to reflect a more logical flow.
* Editing commit messages before pushing them to a remote repository

**Syntax:**

```bash
git checkout branch_x
git rebase -i master
```

**In this syntax**:

* This command lists all commits that are about to be moved and prompts you to edit or rearrange them based on your choices. It helps maintain a clean and structured project history.

##### ****2. Non-Interactive Rebase (Standard Rebase)****

* This is the regular rebase command (git rebase `<branch>`), which simply applies your commits onto the target branch without allowing for manual intervention. It’s ideal for straightforward rebasing where you don’t need to modify or review individual commits.
* Updating your feature branch with the latest changes from the main branch.

****Syntax:****

```bash
git checkout <feature-branch>
git rebase <base-branch>
```

****In this syntax:****

* `<feature-branch>` is the branch with the changes you want to rebase.
* `<base-branch>` is the branch you want to rebase your changes onto, typically main or master.

#### When to Use Git Rebase

You can use git rebase in the following situations:

* ****Clean up commit history:**** If you’ve made multiple small commits or fixes that you want to combine into one commit for a cleaner history.
* ****Stay up-to-date with the base branch**** : If you’re working on a feature branch and want to incorporate changes from the master branch into your branch without creating merge commits.
* ****Prepare a branch for merging:**** Before merging a feature branch into the master branch, you can use rebase to make sure your branch’s changes are applied on top of the latest master branch.

![1746390799863](1746390799863.png)

#### Merging vs Rebasing

![1746391592116](1746391592116.png)

| ****Git Rebase****                                                       | ****Git Merge****                                                           |
| ------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------- |
| Rewrites commit history, leading to a cleaner, linear history.                       | Keeps commit history as is, leading to a more complex, branching history.               |
| No merge commit is created, making the history easier to follow.                     | A merge commit is created, which can clutter the history.                               |
| Can be used to update a feature branch with the latest changes from the base branch. | Often used to integrate feature branches into the main branch.                          |
| Best for cleaning up commit history before merging.                                  | Best for preserving history and when you want to maintain the exact sequence of events. |

#### Git Cherry pick

![1746391404822](1746391404822.png)

git **cherry-pick** in git means choosing a commit from one branch and applying it to another branch. This is in contrast with other ways such as **merge** and **rebases** which normally apply many commits into another branch.

git cherry-pick is just like Rebasing an advanced concept and also a powerful command. It is mainly used if you don’t want to merge the whole branch and you want some of the commits.

* Before cherry pick

![1746389939141](1746389939141.png)

* After Cherry pick

![1746389948319](1746389948319.png)

The command for Cherry-pick is as follows:

```bash
git cherry-pick<commit-hash>
```

#### Some important Use Cases of Cherry-pick

The following are some common applications of Cherry-Pick:

1. If you by mistake make a commit in an incorrect branch, then using cherry-pick you can apply the required changes.
2. Suppose when the same data structure is to be used by both the frontend and backend of a project. Then a developer can use cherry-pick to pick the commit and use it to his/her part of the project.
3. At the point when a bug is found it is critical to convey a fix to end clients as fast as could be expected.
4. Some of the time a component branch might go old and not get converged into the main branch and the request might get closed, but since git never loses those commits, it can be cherry-picked and it would be back.

#### How to use cherry-pick?

To demonstrate how to use `git cherry-pick` let us assume we have a repository with the following branch state:

```css
    a - b - c - d   Main
         \
           e - f - g Feature
```

`git cherry-pick` usage is straight forward and can be executed like:

```bash
git cherry-pick commitSha
```

In this example `commit` Sha is a commit reference. You can find a commit reference by using `git log`. In this example we have constructed lets say we wanted to use commit `f` in `main`. First we ensure that we are working on the `main` branch.

```css
git checkout main
```

Then we execute the cherry-pick with the following command:

```bash
git cherry-pick f
```

Once executed our Git history will look like:

```css
    a - b - c - d - f   Main
         \
           e - f - g Feature
```

The f commit has been successfully picked into the main branch

Prepared with thanks by Kevin Comba
