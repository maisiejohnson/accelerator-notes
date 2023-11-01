# GIT: REMOTES

- To be able to collaborate on any git project you need to know how to manage your remote repos.
- **Remote repositories** are versions of your project that are hosted on the internet or on a network somewhere.
- You can have several remote repositories, each of which is generally either read-only or read/write for you.
- Collaborating with others involves pushing data to and pulling from these remote repositories when you need to share work.

## Pulling from Your Remotes

- To fetch and then merge changes from a remote into your current work use the command:
  ```console
  $ git pull <-remote-name->
  ```
- If you have cloned a remote repo using `git clone <-url->` then you only need to use `git pull`, (i.e., remote-name not necessary)

## Pushing to Your Remotes

- When you have your project at a point that you want to share, you have to push it upstream.
- The command for this is:
  ```console
  $ git push <-remote-name-> <-branch->
  ```
- If there is only one branch and the repo is one that you have cloned then you only need to run `git push` (i.e., no remote name or branch name necessary).
