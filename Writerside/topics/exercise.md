# exercise

### **Exercise 1: Set Up a GitHub Repository and Local Setup**

1. **Create a GitHub repository** :

* Go to GitHub and create a new repository. Name it something like `git-workshop-project`.
* Clone the repository to your local machine.

1. **Create the initial files** :

* Create an `index.html` and `styles.css` file in the repository.
* Initialize the files with basic HTML and CSS content.
* Commit the changes to your repository.

---

### **Exercise 2: Implement the Feature Branch Workflow**

#### Task: {id="task_1"}

You are part of a team developing a webpage. Each feature needs to be developed in a separate branch.

1. **Create a new feature branch** for the header section of the webpage.
2. **Edit `index.html`** : Add a header section in HTML.
3. **Edit `styles.css`** : Add styles for the header.
4. **Commit and push the feature** to GitHub.
5. **Create a Pull Request (PR)** in GitHub to merge your feature branch into `main`.

---

### **Exercise 3: Resolve Pull Request Feedback**

1. **Review the Pull Request** : Imagine your teammate reviews your pull request and leaves feedback suggesting a change in the header background color.
2. **Edit the `styles.css`** file: Modify the header background color according to the feedback.
3. **Commit the changes** and push them back to the feature branch.
4. **Check the pull request** on GitHub. Ensure your changes appear in the PR, and wait for approval to merge it into `main`.

---

### **Exercise 4: Use Git Rebase to Keep Feature Branch Up to Date**

#### Task: {id="task_2"}

The `main` branch has received some changes while you're working on your feature branch. You want to bring your feature branch up to date with the latest changes from `main`.

1. **Switch to your feature branch** .
2. **Fetch the latest changes** from the `main` branch.
3. **Rebase your feature branch** onto the latest `main`.
4. **Resolve any merge conflicts** that arise during the rebase.
5. **Push your changes** back to GitHub.

---

### **Exercise 5: Cherry-Pick a Commit from Another Branch**

#### Task: {id="task_3"}

There was a commit in the `feature/footer` branch that adds a footer to the page, and you want to apply this change to your `feature/header` branch without merging the entire branch.

1. **Identify the commit hash** you want to cherry-pick.
2. **Cherry-pick the commit** onto your current branch.
3. **Resolve any conflicts** and commit the changes.
4. **Push the changes** to GitHub.

---

### **Exercise 6: Use GitFlow Workflow for Feature and Release Branches**

#### Task: {id="task_4"}

You are tasked with following GitFlow to manage your feature and release branches.

1. **Initialize GitFlow** in your repository.
2. **Create a new feature branch** for a new feature (e.g., adding a sidebar).
3. **Develop the feature** : Make the necessary changes in the `index.html` and `styles.css`.
4. **Finish the feature** once done and merge it into `develop`.
5. **Create a release branch** to prepare for deployment.
6. **Merge the release branch** back into `main` and tag the release.

---

### **Exercise 7: Handle Hotfix Branches in GitFlow**

#### Task: {id="task_5"}

You are tasked with fixing a critical bug in the `main` branch, so you need to create a hotfix branch.

1. **Create a hotfix branch** from `main`.
2. **Fix the issue** in the `header` section (e.g., remove an incorrect HTML tag).
3. **Commit and finish the hotfix** .
4. **Push the changes** to the remote repository.

---

### **Exercise 8: Forking Workflow (Collaborating on Open Source)**

#### Task:

You will practice the Forking Workflow commonly used in open-source projects.

1. **Fork a GitHub repository** (e.g., a simple HTML/CSS project) to your GitHub account.
2. **Clone your fork** to your local machine.
3. **Create a feature branch** to add a new section to the webpage.
4. **Make changes** to the `index.html` file.
5. **Push your changes** to your fork.
6. **Open a pull request** from your fork's feature branch to the original repository.

---