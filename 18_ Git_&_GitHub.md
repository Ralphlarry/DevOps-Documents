##	Scenario (Real Job Ticket):
##	You joined the “CodeTrack” project. Your manager wants:
1.	A clean initial commit with starter UI files
2.	A second commit after you follow product instructions in index.html
3.	A basic deployment to an EC2 web server (Nginx)

##	Learning Objectives
##   You will learn to:
•	Inspect repo state with git status
•	Stage changes properly (git add . vs git add <file>)
•	Create meaningful commits (two commits minimum)
•	Verify history using 
	
	git log --oneline
	
•	Deploy a static website to EC2 using Nginx (industry simulation)

##  Prerequisites
•	Assignment 1 completed: CodeTrack exists and is a Git repo (.git folder present)
•	Git installed: 
	
	git --version
	
•	Basic file editing (VS Code / Notepad / Nano)
•	AWS EC2 access for deployment task (Task 7)



##  Notes / Assumptions
##    •	Your repo is named CodeTrack and already initialized with Git.
##    •	Default branch might be master or main depending on Git version/settings (both are okay).
##    •	For EC2, you may use Ubuntu or Amazon Linux. Steps provided for both.

##  Task 1 — Verify Git Setup + Enter the Repo
##  Goal: Confirm Git works and you are inside the right folder.
##  Steps (copy-paste)
##    1.	Check Git:
    git --version
    
##    2.	Go to your CodeTrack folder:
##  macOS/Linux/Git Bash:
    cd ~/projects/CodeTrack
    pwd
    
##  Windows PowerShell (example path):
    cd C:\Users\<YourUser>\projects\CodeTrack
    cd
    
##  3.	Confirm it’s a Git repo:
    git status
    
##  ✅ Expected: You see a status message and no “not a git repository” error.

##  Industry Note
##  Half of Git mistakes happen because people run commands in the wrong folder. Pros always verify with pwd + git status.

##  Task 2 — Create index.html and style.css
##  Goal: Create two files and confirm they exist.

##  Steps
##  macOS/Linux/Git Bash:
    touch index.html style.css
    ls
    
##  Windows PowerShell (no touch):
    echo. > index.html
    echo. > style.css
    dir
    
##  ✅ Expected: You see both files in the directory listing.

##  Industry Note
##  This simulates the first step of a frontend ticket: scaffold basic files before you start development.

##  Task 3 — Add Starter Content (Two Options)
##  Goal: Put real HTML/CSS content in the files.
##    •	Open GitHub repo: Week-2---Git-GitHub-Assignment
##    •	Copy content from their index.html and style.css
##    •	Paste into your local files

##  Industry Note
##  Teams often give a starter template repo. Your job is to pull/apply it and then start making controlled commits.

##  Task 4 — Track and Stage Files Correctly
##  Goal: See untracked files, then stage them.
##  Steps
##  1.	Check status:
    git status
    
##  ✅ Expected: index.html and style.css appear as untracked.
##  2.	Stage files (choose one approach):
##  Approach 1 (recommended for beginners now):
    git add index.html
    git add style.css
    
##  Approach 2 (bulk stage):
    git add .
    
##  3.	Verify staged:
    git status
    
##  ✅ Expected: Under Changes to be committed you see new file: index.html and new file: style.css

##  Industry Note
##  Staging is how you control exactly what goes into a commit. Professionals avoid “accidental commits” by staging intentionally.

##  Task 5 — Create the First Commit (Clean Initial Commit)
##  Goal: Make your first commit with a meaningful message.
##  Steps:
    git commit -m "Initial UI scaffold: add index.html and style.css"

##  Verify history:
    git log --oneline

##  ✅ Expected: 1 commit appears.
##  Industry Note
##  Commit messages should read like a work log. “Initial UI scaffold…” tells reviewers what happened.

##  Task 6 — Modify index.html and Make a Second Commit (Controlled Change)
##  Goal: Simulate a real “small change” ticket and commit it separately.
##  Steps:
##  1.	Open index.html in browser:

##  2.	Follow the instructions inside index.html (from the comment block):
##    •	Change Student Name & Group Name
##    •	Save file and refresh browser

##  3.	Confirm Git sees modification:
    git status
    
##  4.	Stage only the file you changed:
    git add index.html
    git status
    
##  5.	Commit with a meaningful message:
    git commit -m "Update homepage content: heading, tagline, CTA button"

##  6.	Verify history:
    git log –oneline

##  Industry Note
##  Multiple commits are good practice: one commit for scaffolding, one for the feature change. This makes PR review and rollback easier.

##  Task 7 — Deploy to EC2 with Nginx (Static Website)
##  Goal: Deploy your CodeTrack site to a live server.
##  Required EC2 Setup (must be true)
##    •	EC2 instance running (Ubuntu or Amazon Linux)
##    •	Security Group allows:
##    •	SSH (22) from your IP
##    •	HTTP (80) from anywhere (0.0.0.0/0) for testing

##    Step A — SSH into EC2
    ssh -i your-key.pem ubuntu@<EC2_PUBLIC_IP>
##  (For Amazon Linux, user is often ec2-user)

##  follow as below steps, you already mastered now from the Linux Section.
##  Step B — Install & Start Nginx
##  Step C — Copy your files to EC2 (from your local machine)
##  Step D — Move files into Nginx web root (on EC2)
##  Step E — Validate from your browser

##  Open:
    http://<EC2_PUBLIC_IP>

##  ✅ You should see your CodeTrack page.
##  Industry Note
##  This simulates a classic DevOps flow: build locally → commit changes → deploy to server. Even with CI/CD later, this helps you understand what pipelines automate.

##    •	Your default branch is either main or master. Use whichever exists.
##    •	If you see neither main nor master, you will identify your default branch via git branch.

##  Confirm Repo State and Default Branch
##  Goal: Ensure you’re starting clean from the default branch.
##  Steps
    cd path/to/CodeTrack
    git status
    git branch

##  ✅ Expected:
##    •	git status shows a clean working tree (or at least no unexpected changes)
##    •	You can see your branches and identify the default branch
##  If you are not on your default branch:
##  If default is main:
    git checkout main / git switch main

##  If default is master:
    git checkout master / git switch master

##  Re-check:
    git status
    git branch

##  Industry Note
##  Professional teams start feature work from a clean default branch to reduce merge conflicts and accidental changes.

##  Create and Switch to a Feature Branch
##  Goal: Create a branch named exactly: feature/contact-page
##  Steps:
    git checkout -b feature/contact-page
    git branch

##  ✅ Expected: You see:
##    •	* feature/contact-page

##  Industry Note
##  Feature branches are standard in GitHub Flow: isolate work → review → merge safely.

##  Add contact.html on the Feature Branch
##  Goal: Create contact.html and commit it on the branch.
##  Steps:
##  Create the file:
##  macOS/Linux/Git Bash:
    touch contact.html && cd contact.html

##  Windows PowerShell:
    vi contact.html

##  Paste this content into contact.html:

```
1.	html
2.	<!doctype html>
3.	<html lang="en">
4.	<head>
5.	  <meta charset="utf-8" />
6.	  <meta name="viewport" content="width=device-width, initial-scale=1" />
7.	  <title>Contact - CodeTrack</title>
8.	  <link rel="stylesheet" href="style.css" />
9.	</head>
10.	<body>
11.	  <h1>Contact Us</h1>
12.	 
13.	  <p>
14.	    To join <strong>DMI Cohort 3</strong>, join the WhatsApp community here:
15.	    <a
16.	      href="https://chat.whatsapp.com/LSQpMsW9suFAS54DKtLcgE"
17.	      target="_blank"
18.	      rel="noopener noreferrer"
19.	      aria-label="Join DMI Cohort 3 WhatsApp Community (opens in a new tab)"
20.	    >
21.	      Join WhatsApp Community
22.	    </a>
23.	  </p>
24.	 
25.	  <p>
26.	    Learn more about DMI here:
27.	    <a
28.	      href="https://pravinmishra.com/"
29.	      target="_blank"
30.	      rel="noopener noreferrer"
31.	      aria-label="Visit Pravin Mishra website (opens in a new tab)"
32.	    >
33.	      pravinmishra.com
34.	    </a>
35.	  </p>
36.	</body>
37.	</html>

```

##  Verify file exists:
    ls

##  Stage and commit:
    git status
    git add contact.html
    git commit -m "feat(contact): add Contact page"

##  Industry Note
##  A dedicated commit for a new page is “atomic” and makes reviews clean. Reviewers can approve it independently.

##  Add Contact Link to index.html (Still on Branch)
##  Goal: Add navigation link to Contact page and commit that separately.

##  Step-by-step
##  1.	Open index.html in your editor.
##  2.	Find the existing paragraph with class playlist-line (the one containing the YouTube playlist link).
##  3.	Insert the new paragraph directly below it:

```
<p class="playlist-line">
	    Want to reach us? Visit the
	    <a href="contact.html">Contact Page</a>.
</p>
```
##  Save the file.

##  Confirm changes:
    git status
    
##  Stage + commit:
    git add index.html
    git commit -m "feat(nav): add Contact Page link"

##  Industry Note
##  This is how real teams keep changes reviewable: one commit for the page, one commit for navigation linking.

##  Verify Isolation (Prove Main is Unchanged)
##  Goal: Demonstrate your feature work does not affect main/master until merged.
##  Steps:
##  Switch back to default branch:
##  If default is main:
    git checkout main / git switch main

##  If default is master:
    git checkout master / git switch master

##  Verify file absence:
    ls
    
##  ✅ Expected:
##    •	contact.html should NOT exist on default branch (before merge)

##  Verify homepage does NOT include the link yet:
##    •	Open index.html in your browser on the default branch
##    •	Confirm the “Contact Page” link is missing

##  Industry Note
##  This is the core promise of branching: safe parallel development without breaking the stable branch.

##  Merge Feature Branch into Default Branch
##  Goal: Merge your feature branch into main/master and validate results.
##  Steps
##  Merge:
    git merge feature/contact-page

##  Verify:
    ls

##  ✅ Now contact.html should be present.
##  Open index.html in your browser:
##    •	Contact link should appear 
##    •	Click it → Contact page should open 

##  Industry Note
##  Merging is how teams deliver completed work back to stable. Verification after merge is a real deployment mindset.

##  Inspect History (Graph View)
##  Goal: Show your branch and merge history.
##  Steps
    git log –oneline –graph –decorate –all

##  Industry Note
##  Graph logs help in debugging: “What got merged when?”, “Which commit introduced the change?”


##  Optional Cleanup (Delete Feature Branch)
##  Goal: Remove merged branch locally (good hygiene).
##  Steps:
    git branch -d feature/contact-page
    git branch
    
##  ✅ Expected: branch is deleted and no longer listed.






____________________________________________________________________________________________________________________________________________________________________________



##  Scenario (Real Job Ticket)
##  You’re joining an open-source style team workflow. Your task is to contribute one small change to the shared repository using a standard collaboration process:
##  ✅ Fork → ✅ Clone → ✅ Create branch → ✅ Make change → ✅ Sync with upstream → ✅ Push → ✅ Pull Request

##  Upstream repo (original):
##    •	pravinmishraaws/devops-micro-internship-interviews
##  You will fork it to your account and submit a PR back to upstream.

##  Notes / Assumptions (Important Fixes)
##  Your draft had a few mismatches; this assignment corrects them:
##    •	Repo name is devops-micro-internship-interviews .
##    •	You must clone your fork, not the upstream repo directly.
##    •	You will edit ONE target file only (recommended: pull_request.md OR README.md).
##  I’m standardizing this assignment to edit pull_request.md because your instruction explicitly mentioned it.
##    •	Your commit message and PR target must reference the correct repo: devops-micro-internship-interviews.

##  Fork the Upstream Repo
##  Goal: Fork upstream repo into your GitHub account.
##  Steps

##  Open the upstream repo on GitHub:
##    •	pravinmishraaws/devops-micro-internship-interviews

##  Click Fork → Create fork
##  ✅ Expected outcome:
##    •	You now have: yourusername/devops-micro-internship-interviews

##  Industry Note
##  Forks are common in open-source collaboration: you don’t get direct write access to the upstream repo.

##  Authenticate GitHub from Terminal (SSH Recommended)
##  Goal: Your terminal can talk to GitHub without password issues.

##  HTTPS with Personal Access Token (PAT)
##  Step A1 — Create a Personal Access Token (PAT)
##  1.	Login to GitHub
##  2.	Click your profile picture (top-right) → Settings
##  3.	Left menu → Developer settings
##  4.	Personal access tokens → Tokens (classic)
##  5.	Click Generate new token → Generate new token (classic)

##  Fill token details:
##    •	Note: DMI-Git-HTTPS
##    •	Expiration: 30 days (or 90 days if you prefer)
##    •	Scopes (Permissions):  repo

##  (This is enough for private/public repo operations. If the repo is public-only, public_repo can work, but keep it simple: use repo.)
##  6.	Click Generate token
##  7.	Copy the token immediately (you won’t see it again)

##  Expected outcome: You have a token that looks like: ghp_XXXXXXXXXXXXXXXXXXXX

##  Step A2 — Store Credentials Safely on Your Machine
##  Pick based on OS.

##  macOS (Recommended)
    git config --global credential.helper osxkeychain

##  Windows (Recommended)
    git config --global credential.helper manager

##  Linux (Recommended)
##  If you have GNOME Keyring:
    git config --global credential.helper /usr/lib/git-core/git-credential-libsecret

##  If that’s not available, use cache (temporary):
    git config --global credential.helper cache
    git config --global credential.helper 'cache --timeout=36000'

##  Expected outcome: Git will remember your token (depending on OS helper).

##  Step A3 — Test HTTPS Authentication
##  1.	Make sure your origin is HTTPS:
    git remote -v

##  If origin is SSH but you want HTTPS, set it:
    git remote set-url origin https://github.com/<yourusername>/devops-micro-internship-interviews.git

##  2.	Test a push (best test):
    git push

##  When prompted:
##    •	Username: your GitHub username
##    •	Password: paste your Personal Access Token (PAT) (NOT your GitHub password)
##   Expected outcome: Push succeeds without “authentication failed”.

##  Clone Your Fork Locally + Setup Remotes
##  Goal: You have a local copy where:
##    •	origin = your fork
##    •	upstream = original repository

##  Steps
##  1.	Clone your fork (IMPORTANT):
    git clone https://github.com/yourusername/devops-micro-internship-interviews.git
    cd devops-micro-internship-interviews

##  Confirm origin:
    git remote -v

##  ✅ origin should point to yourusername/...
##  3.	Add upstream:
    git remote add upstream https://github.com/pravinmishraaws/devops-micro-internship-interviews.git
    git remote -v

##  ✅ Expected outcome:
##    •	origin → your fork
##    •	upstream → pravinmishraaws repo

##  Industry Note
##  This is the standard model for contributions:
##    •	Pull updates from upstream
##    •	Push your work to origin
##    •	PR from origin branch → upstream main

##  Create Feature Branch + Make Your Change
##  Goal: Create a branch and update only your entry in the student list.
##  Steps
##  1.	Create branch:
    git checkout -b feature-readme-update

##  2.	Open pull_request.md and add your name at the end of the student list:
##  •	✅ Add your name at the end only
##  •	❌ Do not edit/delete anyone else
##  •	Follow format exactly:
##  Student List
##  Full Name — Group <Group Name/Number>

##  Example entry:
##  Pravin Mishra — Group 1

##  3.	Confirm file change:
    git status

##  4.	Stage and commit:
    git add pull_request.md
    git commit -m "docs: add my name to student list"

##  Industry Note
##  Small, single-purpose commits make reviews easier. “One change per commit” is a professional habit.

##  Sync with Upstream and Push to Your Fork
##  Goal: Make sure your fork is up-to-date with upstream before PR.
##  Steps
##  1.	Fetch upstream:
    git fetch upstream

##  2.	Switch to default branch (main/master):
    git checkout main

##  If your default is master:
    git checkout master

##  3.	Merge upstream changes into your local default branch:
    git merge upstream/main
    
##  (If default is master, upstream might still be main. Most likely it’s main.)
##  4.	Switch back to feature branch:
    git checkout feature-readme-update

##  5.	Rebase (optional but recommended):
    git rebase main

##  6.	Push your feature branch to origin:
    git push -u origin feature-readme-update

##  ✅ Expected outcome:
##  •	Your branch exists on GitHub under your fork

##  Industry Note
##  Upstream moves fast in real teams. Syncing prevents “merge conflicts” and keeps PR clean.

##  Create a Pull Request (PR) to Upstream
##  Goal: Open a PR from your fork branch → upstream main.
##  Steps
##  1.	Go to your fork on GitHub:
    github.com/yourusername/devops-micro-internship-interviews

##  2.	Click Compare & pull request

##  3.	Ensure PR target is correct:
##    •	Base repository: pravinmishraaws/devops-micro-internship-interviews
##    •	Base branch: main
##    •	Head repository: yourusername/devops-micro-internship-interviews
##    •	Compare branch: feature-readme-update

##  4.	PR Title:
    docs: add my name to student list

##  5.	PR Body (paste this):
    This PR adds my name to the Student List in pull_request.md as part of the DMI GitHub collaboration assignment.

##  6.	Create Pull Request
##  Industry Note
##  PRs are how teams review work, enforce standards, and keep the main branch stable.

