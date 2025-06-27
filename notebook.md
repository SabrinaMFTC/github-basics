# Tutorial for GitHub basics

## Summary

I. [Creating an Account](#i---creating-an-account)<br>
II. [Creating a Repository](#ii---creating-a-repository)<br>
III. [Creating a Token](#iii---creating-a-token)<br>
IV. [Cloning a Repository](#iv-cloning-a-repository)<br>
V. [Adding, Commiting and Pushing](#v-adding-commiting-and-pushing)<br>
VI. [Updating your Local Repository](#vi-updating-your-local-repository)<br>

---

## I. Creating an Account

1 - First, create an account on [GitHub](https://github.com/).

2 - After created, access your account.

## II. Creating a Repository

3 - Create a repository.

![img01](/assets/img01.png)

4 - Name the repository, configure it as you wish - for now, let's make it private and add a README.

![img02](/assets/img02.png)

## III. Creating a Token

5 - Since the repo is private, you will need to add your Git credentials. Since 2021, GitHub doesn't accept password as authentication method. So you will need to create a **token**:

5.1 - On the right upper corner, click on your `Profile Picture > Settings`

![img05](/assets/img05.png)

5.2 - On the left side bar, roll until the end of it and click on `<> Developer settings`

![img06](/assets/img06.png)

5.3 - On the left side bar, click on `Personal access tokens > Tokens (classic)` to create an authentication token.

![img07](/assets/img07.png)

5.4 - Click on `Generate new token`.

![img08](/assets/img08.png)

5.5 - Choose `Generate new token (classic)` to use it as general use.

![img09](/assets/img09.png)

5.6 - On `Note`, you can give the token a name that indicates its usage or simply a generic name. You can also choose the expiration date of this token and select what functionaties it will serve. For the basic usage, you can check just the first scope (repo) and click on `Generate token` in the end of the page.

![img10](/assets/img10.png)

5.7 - **Make sure to save your token somewhere safe**, because you will not be able to access it again once you close that page (you can always generate a new one if needed).

![img11](/assets/img11.png)

## IV. Cloning a Repository

6 - Back to your repo, click on `<> Code` and copy the url of your repo.

![img03](/assets/img03.png)

7 - Open a terminal and clone your repo in the desired location, using

```bash
git clone <repo_url>
```

![img04](/assets/img04.png)

8 - Insert your credentials (**username** and **token**) and hit `Enter`.

![img12](/assets/img12.png)

8 - Move into your repo and check that it's a Git repository, using:

```bash
git status
```

8.1 - If it's a Git repo, you should see informations about the `branch` you currently are in and also the status of your repo (for example, it's updated or not).

![img13](/assets/img13.png)

## V. Adding, Commiting and Pushing

9 - Now let's create a new file in our repo. You can choose whatever method to create a file you preffer (vim, nano, touch) and then use `git status` again:

![img14](/assets/img14.png)

10 - You should see that Git is tracking the changes made. In this case, Git says that there's an untracked file (the file you just created).

11 - To **add** that file to your repo, you need to type:

```bash
git add <fileName>
```

> **TIP:** If you made changes into different files, you add all of them at once using:

```bash
git add .
```

12 - This command moves the file you added to a **staging area**, where the changes moved there are not yet commited to your repo, but they are in a pre-commit area.

13 - You can use `git status` again to check that the file was indeed moved to this staging area and are ready to be commited:

![img15](/assets/img15.png)

14 - Now, you can **commit** the changes you made using:

```bash
git commit -m "your-commit-message"
```

> **TIP:** You will need to add a commit message that indicates what change was made, so it's easier for you and others to know what was changed in that specific point. You can check the best practices when it comes to a commit message [here](https://www.conventionalcommits.org/en/v1.0.0/).

![img16](/assets/img16.png)

15 - You can use `git status`again to check that the change was moved from the staging area and commited. Git will tell you that the branch you currently are in (in this case, the `main` branch, which is the default branch every repo starts in) is ahead of `origin/main` by 1 commit, since you only made 1 commit so far.

![img17](/assets/img17.png)

16 - Finally, to **push** that change in your repo, you need to enter a last command:

```bash
git push
```

16.1 - You will need to insert your Git credentials again (**username** and **token**).

![img18](/assets/img18.png)

17 - You can check that the change you made was correctly done accessing your repo on the browser or using `git status`:

![img20](/assets/img20.png)
![img19](/assets/img19.png)

17.1 - Git will tell you that your branch is up to date with `origin/main`.

## VI. Updating your Local Repository

18 - It's a good practice to always use the command

```bash
git pull
```

> **TIP:** Use `git pull` before you start working on new changes in your local repo, so if someone else (or you, in another machine) made changes to the repo, it will be updated.

![img21](/assets/img21.png)

## VII. Merging

19 - Let's suppose someone else (or you, in another machine) made changes to the repo at the same time you did or that you made changes after and forgot to `git pull` beforehand. In that case, we will have a **merge conflict** that needs to be resolved.

20 - As an example, I changed the `helloWorld.txt` file in my local repo:

![img22](/assets/img22.png)

21 - Meanwhile, someone else changed the same file in their local repo:

![img23](/assets/img23.png)

22 - If you try to add, commit and push your local change to the repo, Git will reject the commit saying:

![img24](/assets/img24.png)

```bash
 ! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'https://github.com/galaxdriel-git/example-repo.git'
hint: Updates were rejected because the remote contains work that you do not
hint: have locally. This is usually caused by another repository pushing to
hint: the same ref. If you want to integrate the remote changes, use
hint: 'git pull' before pushing again.
```

23 - If you try to **pull** now, using `git pull`, Git will tell you that you need to reconcile the divergent branches (the one you are currently working on, in your local repo and the one that was commited before your change that you didn't pull):

![img25](/assets/img25.png)

24 - You can try to solve this conflict following Git's instructions - type `git config pull.rebase false` in order to merge the changes made by you and the other person:

```bash
git config pull.rebase false
```

25 - Now you can try to `git pull` again, but depending on the change made, it can fail. If you check your file, you should see the version you have locally, marked with `<<<<<<< HEAD` and the remote version, that starts after `=======`:

![img26](/assets/img26.png)

25 - Now you can edit the file, keeping your **local version**, the **remote one** on GitHub or **combining** both. Then you can save the file and add, commit and push normally. Finally, you can check if the commit was successfully made, using `git status`:

![img27](/assets/img27.png)

26 - We learned how to solve merge conflits. However, the ideal would be that each person would work in a different branch, which we'll learn now.

## VIII. Branches

27 - By default, everyone working on a repo starts in the `main` branch of the repo. However, the best practice is for each person to work on their own branch, to avoid conflicts like the one we just experienced.

28 - In order to create a new branch, use:

```bash
git checkout -b "<your-branch-name>"
```

![img28](/assets/img28.png)

29 - You will be automatically moved into the new branch, which you can check by typing `git status`:

![img29](/assets/img29.png)

30 - Now every change you make in any file or directory inside the repo will only be made into your own branch.

31 - You can create a new file, for example, add, commit and push it to the your branch.

![img30](/assets/img30.png)

32 - Since your branch is not yet connected to the `main` branch, Git tells you that you need to push the current branch and set the remote as upstream. For that, you need to type:

```bash
git push --set-upstream origin <your-branch-name>
```

![img31](/assets/img31.png)

33 - Now your branch is connected to the `main` branch in the remote repo.

34 - Back on the browser, if you click on `main`, you can see the branch you created:

![img32](/assets/img32.png)

35 - If you switch to the branch `sabrina`, you will see the file `testingBranches.md`, which we created only in that new branch. Git also informs you that this branch is `1 commit ahead of main`:

![img33](/assets/img33.png)

36 - If you switch back to the `main` branch, you will notice that the file `testingBranches.md`doesn't exist there:

![img34](/assets/img34.png)

37 - If you go to your branch `sabrina` and click on `Contribute`, you can **open a pull request** if you wish to merge your branch to the `main` branch:

![img35](/assets/img35.png)

38 - You can then click on `Create pull request`:

![img36](/assets/img36.png)

39 - If there are no conflicts with the base branch (`main`), you can click on `Merge pull request`:

![img37](/assets/img37.png)

40 - You should see the message `Pull requets successfully merged and closed`:

![img38](/assets/img38.png)

41 - Now, going back to the initial repo page, you should see that the file (or any other change you made in your branch) is also in the `main` branch:

![img39](/assets/img39.png)
