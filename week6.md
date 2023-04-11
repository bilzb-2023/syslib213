# Week 6: Learn Git and GitHub

# Setup Git and GitHub (Week 6)
---

## Description
---

This week we start using Git and GitHub to document our processes.
Documenting our work, as we do it, is a great way to develop work flows.

### Tasks
---

- [x] I created an account on GitHub (https://github.com/) using Dr. Burns' ins>
- [x] I created a new repository on GitHub named syslib213

At this point, I learned that I tested positive for COVID-19,
completely upending everything family, work, life. I spent the
next 1-2 weeks recovering. I kept thinking about the assignment,
though. Nuts, I know, but I just couldn't concentrate. I did
understand that "Covid-brain" does exist and explains why I wasn't
able to just pick up where I left off. I was in the middle of this
assignment when I realized that the only to figure out what I did
is to start over.

When I returned, I realized that while I'd setup my GitHub account,
I hadn't configured Git on the remote server (Linux).

- [x] I setup git on my Linux server.
- [x] I configured git using these commands:

git config --global user.name "First Name Last Name"
git config --global user.email "firstlast@example.com"
git config --global core.editor nano
git config --global init.defaultBranch main

I then checked the settings using this command: git config --list

I cloned the GitHub repo git@github.com:bilzb-2023/syslib213.git to
the Linux server using this command from the
bbilz@syslib-2023:~/repos$ git clone git@github.com:bilzb-2023/syslib213.git

I open nano and create syslib213

I add syslib213 to git by using this command: gitadd syslib213

I then commit syslib213 to git with a comment:
git commit -m "created file"

I then use this command to push the update to git:
git push origin main
 
From the bbilz@syslib-2023:~/repos, I enter ls to see the files in the
repos directory. There are listed: SetupGitandGitHub.md syslib syslib213

I then enter this command to change the file extension to .md:
git mv syslib213 syslib213.md

Add the new name to git: git add .

Commit it to git: git commit -m "added md file extension"

Push it to git:  git push origin main

This process was also completed first with the README.md file and served
as an example of how to do this with future weekly updates.


---


I created a directory on my Linux server called repos and cloned my repo
inside that directory.

- [x] I used the cloned repository to add documentation in Markdown.

---

The process for doing this weekly:

-- [] Open the Linux remote server on my computer.
-- [] Create a new document in Nano for each week.
-- [] Commit the file using this command: git add document name
-- [] Commit changes and add message with: git commit -m "add message in quotes"
-- [] Push changes to remote repo with: git push origin main

In short, going forward, each time I make edits or add new files,
simply repeat the following commands to sync your local repo to the
GitHub repo:


1. git add .
2. git commit -m "add message in quotes"
3. git push origin main

---


Note: Work in the Linux server and not in GitHub. The purpose is to learn
how to create, update, and push the updates to GitHub.

