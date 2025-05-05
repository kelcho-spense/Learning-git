# Collaborating workflows (syncing)


### `git fetch` :

The `git fetch` command downloads commits, files, and refs from a remote repository into your local repo

* `git fetch <remote>` : Fetch all of the branches from the repository. This also downloads all of the required commits and files from the other repository.
* `git fetch <remote> <branch>` : Same as the above command, but only fetch the specified branch.
* `git fetch --all` : A power move which fetches all registered remotes and their branches

### `git push` :

 is most commonly used to publish an upload local changes to a central repository. After a local repository has been modified a push is executed to share the modifications with remote team members.

![Using git push to publish changes](https://wac-cdn.atlassian.com/dam/jcr:0d181327-3fb0-44ec-9ab4-d6dea0fd406f/01%20Git%20push%20discussion.svg?cdnVersion=2688)

The above diagram shows what happens when your local `main` has progressed past the central repository’s `main` and you publish changes by running `git push origin main`

The `git push` command is used to upload local repository content to a remote repository

* `git push <remote> <branch>` : Push the specified branch to , along with all of the necessary commits and internal objects. This creates a local branch in the destination repository.
* `git push <remote> --force` : Same as the above command, but force the push even if it results in a non-fast-forward merge
* Deleting a remote branch or tag : The fully delete a branch, it must be deleted locally and also remotely.

  ```bash
  git branch -D branch_name
  git push origin :branch_name
  ```

### `git pull` :

The `git pull` command is used to fetch and download content from a remote repository and immediately update the local repository to match that content.

#### How it works {id="how-it-works_2"}

The `git pull` command first runs `git fetch` which downloads content from the specified remote repository. Then a `git merge` is executed to merge the remote content refs and heads into a new local merge commit. To better demonstrate the pull and merging process let us consider the following example. Assume we have a repository with a main branch and a remote origin.

![](https://wac-cdn.atlassian.com/dam/jcr:63e58c34-b273-4e48-a6b1-6e3ba4d4a0ea/01%20bubble%20diagram-01.svg?cdnVersion=2688)

In this scenario, `git pull` will download all the changes from the point where the local and main diverged. In this example, that point is E. `git pull` will fetch the diverged remote commits which are A-B-C. The pull process will then create a new local merge commit containing the content of the new diverged remote commits.

![img](https://wac-cdn.atlassian.com/dam/jcr:0269bb2d-eb7f-43d8-80a2-8afa88d11eea/02%20bubble%20diagram-02.svg?cdnVersion=2688)

In the above diagram, we can see the new commit H. This commit is a new merge commit that contains the contents of remote A-B-C commits and has a combined log message. This example is one of a few `git pull` merging strategies. A `--rebase` option can be passed to `git pull` to use a rebase merging strategy instead of a merge commit. The next example will demonstrate how a rebase pull works. Assume that we are at a starting point of our first diagram, and we have executed `git pull --rebase`.

![Central git repo to local git repo](https://wac-cdn.atlassian.com/dam/jcr:d5633068-d448-4140-953e-2ab31553ce10/03%20bubble%20diagram-03-updated@2x%20kopiera.png?cdnVersion=2688)

In this diagram, we can now see that a rebase pull does not create the new H commit. Instead, the rebase has copied the remote commits A--B--C and rewritten the local commits E--F--G to appear after them them in the local origin/main commit history.

### Making a pull request(PR)

![1746394977375](1746394977375.png)

Pull requests are a feature that makes it easier for developers to collaborate using Bitbucket, GitHub, Azure Repos and Gitlab. They provide a user-friendly web interface for discussing proposed changes before integrating them into the official project.

In their simplest form, pull requests are a mechanism for a developer to notify team members that they have completed a feature. Once their feature branch is ready, the developer files a pull request via their Bitbucket account. This lets everybody involved know that they need to review the code and merge it into the `main` branch.

But, the pull request is more than just a notification—it’s a dedicated forum for discussing the proposed feature. If there are any problems with the changes, teammates can post feedback in the pull request and even tweak the feature by pushing follow-up commits. All of this activity is tracked directly inside of the pull request.

![Git workflows: Activity inside a pull request](https://wac-cdn.atlassian.com/dam/jcr:dc1a0821-efd6-4852-b7e6-c3a787656c61/02.svg?cdnVersion=2688)

Compared to other collaboration models, this formal solution for sharing commits makes for a much more streamlined workflow.

#### How PR works

Pull requests can be used in conjunction with the Feature Branch Workflow, the Gitflow Workflow, or the Forking Workflow. But a pull request requires either two distinct branches or two distinct repositories, so they will not work with the Centralized Workflow. Using pull requests with each of these workflows is slightly different, but the general process is as follows:

1. A developer creates the feature in a dedicated branch in their local repo.
2. The developer pushes the branch to a public Bitbucket repository.
3. The developer files a pull request via Bitbucket.
4. The rest of the team reviews the code, discusses it, and alters it.
5. The project maintainer merges the feature into the official repository and closes the pull request.

The rest of this section describes how pull requests can be leveraged against different collaboration workflows.

##### Feature Branch Workflow With Pull Requests

The Feature Branch Workflow uses a shared Bitbucket repository for managing collaboration, and developers create features in isolated branches. But, instead of immediately merging them into `main`, developers should open a pull request to initiate a discussion around the feature before it gets integrated into the main codebase.

![Feature branch workflow](https://wac-cdn.atlassian.com/dam/jcr:8359fb05-ef37-428d-9e45-d0591614a126/02%20Anatomy%20of%20a%20Pull%20Request.svg?cdnVersion=2688)

There is only one public repository in the Feature Branch Workflow, so the pull request’s destination repository and the source repository will always be the same. Typically, the developer will specify their feature branch as the source branch and the `main` branch as the destination branch.

After receiving the pull request, the project maintainer has to decide what to do. If the feature is ready to go, they can simply merge it into `main` and close the pull request. But, if there are problems with the proposed changes, they can post feedback in the pull request. Follow-up commits will show up right next to the relevant comments.

It’s also possible to file a pull request for a feature that is incomplete. For example, if a developer is having trouble implementing a particular requirement, they can file a pull request containing their work-in-progress. Other developers can then provide suggestions inside of the pull request, or even fix the problem themselves with additional commits.

##### Gitflow Workflow With Pull Requests

The Gitflow Workflow is similar to the Feature Branch Workflow, but defines a strict branching model designed around the project release. Adding pull requests to the Gitflow Workflow gives developers a convenient place to talk about a release branch or a maintenance branch while they’re working on it.

![Gitflow workflow](https://wac-cdn.atlassian.com/dam/jcr:50c76de3-6c5b-4adf-9a96-a611cc3dbebc/05.svg?cdnVersion=2688)

![Gitflow workflow](https://wac-cdn.atlassian.com/dam/jcr:a7e725a9-c98e-4a7f-af46-5106b2358d50/03%20Gitflow%20Workflow%20With%20Pull%20Requests.svg?cdnVersion=2688)

The mechanics of pull requests in the Gitflow Workflow are the exact same as the previous section: a developer simply files a pull request when a feature, release, or hotfix branch needs to be reviewed, and the rest of the team will be notified via Bitbucket.

Features are generally merged into the `develop` branch, while release and hotfix branches are merged into both `develop` and `main`. Pull requests can be used to formally manage all of these merges.

##### Forking Workflow With Pull Requests

In the Forking Workflow, a developer pushes a completed feature to *their own* public repository instead of a shared one. After that, they file a pull request to let the project maintainer know that it’s ready for review.

The notification aspect of pull requests is particularly useful in this workflow because the project maintainer has no way of knowing when another developer has added commits to their Bitbucket repository.

![Forking workflow](https://wac-cdn.atlassian.com/dam/jcr:bab8474f-faf7-4538-aa5c-66fb52846583/04%20Forking%20Workflow%20With%20Pull%20Requests.svg?cdnVersion=2688)

Since each developer has their own public repository, the pull request’s source repository will differ from its destination repository. The source repository is the developer’s public repository and the source branch is the one that contains the proposed changes. If the developer is trying to merge the feature into the main codebase, then the destination repository is the official project and the destination branch is `main`.

Pull requests can also be used to collaborate with other developers outside of the official project. For example, if a developer was working on a feature with a teammate, they could file a pull request using the *teammate’s* Bitbucket repository for the destination instead of the official project. They would then use the same feature branch for the source and destination branches.

![Pull requests: Forking workflow](https://wac-cdn.atlassian.com/dam/jcr:0907a594-5786-47fb-87b4-05fc08e0c8dc/08.svg?cdnVersion=2688)

The two developers could discuss and develop the feature inside of the pull request. When they’re done, one of them would file another pull request asking to merge the feature into the official main branch. This kind of flexibility makes pull requests very powerful collaboration tool in the Forking workflow.

##### Example:

---

The example below demonstrates how pull requests can be used in the Forking Workflow. It is equally applicable to developers working in small teams and to a third-party developer contributing to an open source project.

In the example, Mary is a developer, and John is the project maintainer. Both of them have their own public Bitbucket repositories, and John’s contains the official project.

###### Mary forks the official project

![Fork the project](https://wac-cdn.atlassian.com/dam/jcr:8b3d2111-5a88-4802-967c-71f51c248b03/09.svg?cdnVersion=2688)

To start working in the project, Mary first needs to fork John’s Bitbucket repository. She can do this by signing in to Bitbucket, navigating to John’s repository, and clicking the *Fork* button.

![Fork in bitbucket](https://wac-cdn.atlassian.com/dam/jcr:93d2ede4-241e-4296-b403-584d5ee24d8e/10.svg?cdnVersion=2688)

After filling out the name and description for the forked repository, she will have a server-side copy of the project.

###### Mary clones her Bitbucket repository

![Clone the Bitbucket repo](https://wac-cdn.atlassian.com/dam/jcr:4f051d96-8ce7-4aab-af74-b2de38c41443/11.svg?cdnVersion=2688)

Next, Mary needs to clone the Bitbucket repository that she just forked. This will give her a working copy of the project on her local machine. She can do this by running the following command:

```bash
git clone https://user@bitbucket.org/user/repo.git
```

Keep in mind that `git clone` automatically creates an `origin` remote that points back to Mary’s forked repository.

###### Mary develops a new feature

![Develop a new feature](https://wac-cdn.atlassian.com/dam/jcr:f0979362-cf67-413d-bac1-8275e20aea58/12.svg?cdnVersion=2688)

Before she starts writing any code, Mary needs to create a new branch for the feature. This branch is what she will use as the source branch of the pull request.

```css
git checkout -b some-feature
# Edit some code
git commit -a -m "Add first draft of some feature"
```

Mary can use as many commits as she needs to create the feature. And, if the feature’s history is messier than she would like, she can use an interactive rebase to remove or squash unnecessary commits. For larger projects, cleaning up a feature’s history makes it much easier for the project maintainer to see what’s going on in the pull request.

###### Mary pushes the feature to her Bitbucket repository

![Push feature to Bitbucket repository](https://wac-cdn.atlassian.com/dam/jcr:d3a07e01-ad5c-4e11-929a-87c049a27a6b/13.svg?cdnVersion=2688)

After her feature is complete, Mary pushes the feature branch to her own Bitbucket repository (not the official repository) with a simple `git push`:

```bash
git push origin some-branch
```

This makes her changes available to the project maintainer (or any collaborators who might need access to them).

###### Mary creates the pull request

![Create a pull request](https://wac-cdn.atlassian.com/dam/jcr:de06b2f6-5846-4ef2-af0b-4d1fc17fbc16/05%20Mary%20creates%20the%20pull%20request.svg?cdnVersion=2688)

After Bitbucket has her feature branch, Mary can create the pull request through her Bitbucket account by navigating to her forked repository and clicking the *Pull request* button in the top-right corner. The resulting form automatically sets Mary’s repository as the source repository, and it asks her to specify the source branch, the destination repository, and the destination branch.

Mary wants to merge her feature into the main codebase, so the source branch is her feature branch, the destination repository is John’s public repository, and the destination branch is `main`. She’ll also need to provide a title and description for the pull request. If there are other people who need to approve the code besides John, she can enter them in the *Reviewers* field.

![Pull request within Bitbucket](https://wac-cdn.atlassian.com/dam/jcr:494da6fb-45be-4771-b5a1-2cf940959114/06%20Mary%20creates%20the%20pull%20request.png?cdnVersion=2688)

After she creates the pull request, a notification will be sent to John via his Bitbucket feed and (optionally) via email.

###### John reviews the pull request

![Bitbucket pull request](https://wac-cdn.atlassian.com/dam/jcr:1b30ef44-9679-49d1-bc86-8b1a0cf5e241/pull-request-8.png?cdnVersion=2688)

John can access all of the pull requests people have filed by clicking on the *Pull request* tab in his own Bitbucket repository. Clicking on Mary’s pull request will show him a description of the pull request, the feature’s commit history, and a diff of all the changes it contains.

If he thinks the feature is ready to merge into the project, all he has to do is hit the *Merge* button to approve the pull request and merge Mary’s feature into his `main` branch.

But, for this example, let’s say John found a small bug in Mary’s code, and needs her to fix it before merging it in. He can either post a comment to the pull request as a whole, or he can select a specific commit in the feature’s history to comment on.

![Bitbucket comment within pull request](https://wac-cdn.atlassian.com/dam/jcr:6d9007c1-7b42-42e4-a1ca-f7129185c16d/pull-request-9.png?cdnVersion=2688)

###### Mary adds a follow-up commit

If Mary has any questions about the feedback, she can respond inside of the pull request, treating it as a discussion forum for her feature.

To correct the error, Mary adds another commit to her feature branch and pushes it to her Bitbucket repository, just like she did the first time around. This commit is automatically added to the original pull request, and John can review the changes again, right next to his original comment.

###### John accepts the pull request

Finally, John accepts the changes, merges the feature branch into main, and closes the pull request. The feature is now integrated into the project, and any other developers working on it can pull it into their own local repositories using the standard `git pull` command.

### Using branches

 Git branches are effectively a pointer to a snapshot of your changes. When you want to add a new feature or fix a bug—no matter how big or how small—you spawn a new branch to encapsulate your changes. This makes it harder for unstable code to get merged into the main code base, and it gives you the chance to clean up your future's history before merging it into the main branch.

![Git branch](https://wac-cdn.atlassian.com/dam/jcr:a905ddfd-973a-452a-a4ae-f1dd65430027/01%20Git%20branch.svg?cdnVersion=2688)

The diagram above visualizes a repository with two isolated lines of development, one for a little feature, and one for a longer-running feature. By developing them in branches, it’s not only possible to work on both of them in parallel, but it also keeps the `main` branch free from questionable code.

* `git branch` : List all of the branches in your repository. This is synonymous with `git branch --list.`
* `git branch <branch>` : Create a new branch called `＜branch＞`. This does ***not* check** out the new branch.
* `git branch -d <branch>` : Delete the specified branch. This is a “safe” operation in that Git prevents you from deleting the branch if it has unmerged changes.
* `git branch -D <branch>` : Force delete the specified branch, even if it has unmerged changes. This is the command to use if you want to permanently throw away all of the commits associated with a particular line of development.
* `git branch -m <branch>` : Rename the current branch to `＜branch＞`
* `git branch -a` : List all remote branches.
* `git checkout <branch_name> ` : Switches to the specified branch.
* `git checkout -b <branch_name>` : Creates and switches to a new branch in one step.
* **`git merge <branch_name>`** : Merges the specified branch into the current branch.
  **Example** :

```bash
  git merge feature/add-header
```

#### Creating remote branches

So far these examples have all demonstrated local branch operations. The `git branch` command also works on remote branches

```bash
git remote add new-remote-repo https://bitbucket.com/user/repo.git
# Add remote repo to local repo config
git push <new-remote-repo> crazy-experiment~
# pushes the crazy-experiment branch to new-remote-repo
```

### Merge Conflicts

Version control systems are all about managing contributions between multiple distributed authors ( usually developers ). Sometimes multiple developers may try to edit the same content. If Developer A tries to edit code that Developer B is editing a conflict may occur. To alleviate the occurrence of conflicts developers will work in separate isolated branches.

##### Creating a merge conflict

In order to get real familiar with merge conflicts, the next section will simulate a conflict to later examine and resolve. The example will be using a Unix-like command-line Git interface to execute the example simulation.

```scss

$ mkdir git-merge-test
$ cd git-merge-test
$ git init .
$ echo "this is some content to mess with" > merge.txt
$ git add merge.txt
$ git commit -am"we are commiting the inital content"
[main (root-commit) d48e74c] we are commiting the inital content
1 file changed, 1 insertion(+)
create mode 100644 merge.txt
```

This code example executes a sequence of commands that accomplish the following.

* Create a new directory named `git-merge-test,` change to that directory, and initialize it as a new Git repo.
* Create a new text file `merge.txt` with some content in it.
* Add `merge.txt` to the repo and commit it.

Now we have a new repo with one branch `main` and a file `merge.txt` with content in it. Next, we will create a new branch to use as the conflicting merge.

```scss
$ git checkout -b new_branch_to_merge_later
$ echo "totally different content to merge later" > merge.txt
$ git commit -am"edited the content of merge.txt to cause a conflict"
[new_branch_to_merge_later 6282319] edited the content of merge.txt to cause a conflict
1 file changed, 1 insertion(+), 1 deletion(-)
```

The proceeding command sequence achieves the following:

* create and check out a new branch named `new_branch_to_merge_later`
* overwrite the content in `merge.txt`
* commit the new content

With this new branch: `new_branch_to_merge_later` we have created a commit that overrides the content of `merge.txt`

```bash
git checkout main
Switched to branch 'main'
echo "content to append" >> merge.txt
git commit -am"appended content to merge.txt"
[main 24fbe3c] appended content to merge.tx
1 file changed, 1 insertion(+)
```

This chain of commands checks out the `main` branch, appends content to `merge.txt`, and commits it. This now puts our example repo in a state where we have 2 new commits. One in the `main` branch and one in the `new_branch_to_merge_later` branch. At this time lets `git merge new_branch_to_merge_later` and see what happen!

```scss
$ git merge new_branch_to_merge_later
Auto-merging merge.txt
CONFLICT (content): Merge conflict in merge.txt
Automatic merge failed; fix conflicts and then commit the result.
```

BOOM 💥. A conflict appears. Thanks, Git for letting us know about this!

### How to identify merge conflicts

---

As we have experienced from the proceeding example, Git will produce some descriptive output letting us know that a CONFLICT has occcured. We can gain further insight by running the git status command

```bash
$ git status
On branch main
You have unmerged paths.
(fix conflicts and run "git commit")
(use "git merge --abort" to abort the merge)

Unmerged paths:
(use "git add <file>..." to mark resolution)

both modified:   merge.txt
```

The output from `git status` indicates that there are unmerged paths due to a conflict. The `merge.text` file now appears in a modified state. Let's examine the file and see whats modified.

```bash
$ cat merge.txt
<<<<<<< HEAD
this is some content to mess with
content to append
=======
totally different content to merge later
>>>>>>> new_branch_to_merge_later
```

Here we have used the `cat` command to put out the contents of the `merge.txt `file. We can see some strange new additions

* `<<<<<<< HEAD`
* `=======`
* `>>>>>>> new_branch_to_merge_later`

Think of these new lines as "conflict dividers". The `=======` line is the "center" of the conflict. All the content between the center and the `<<<<<<< HEAD` line is content that exists in the current branch main which the `HEAD` ref is pointing to. Alternatively all content between the center and `>>>>>>> new_branch_to_merge_later` is content that is present in our merging branch.

### How to resolve merge conflicts using the command line

---

The most direct way to resolve a merge conflict is to edit the conflicted file. Open the `merge.txt` file in your favorite editor. For our example lets simply remove all the conflict dividers. The modified `merge.txt` content should then look like:

```css
this is some content to mess with
content to append
totally different content to merge later
```

Once the file has been edited use `git add merge.txt` to stage the new merged content. To finalize the merge create a new commit by executing:

```bash
git commit -m "merged and resolved the conflict in merge.txt"
```

Git will see that the conflict has been resolved and creates a new merge commit to finalize the merge.