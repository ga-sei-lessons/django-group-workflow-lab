# Group Git Workflow With Django

How can we have multiple people contributing to the same software project while working as a distributed team?

We've already been using the answer - it is the same system we use to submit homework via Github.

There are multiple ways to use git to manage collaboration -- we are going to be using the "forking" workflow that is one of the most common and frequently used in open source software development.

In this style of workflow:

- One user initializes and owns a central repository
- Each individual working on the project forks that initial repo
- Each individual then clones that forked repo to their local machine
- As commits happen, they are pushed up to the forked repository.
- For these new changes to be added to the central repository code, workers submit pull requests from their forked repositories. The central owner approves or edits these pull requests.

## Our Task

We will be building a Note Taking App collaboratively with Django.

### App Specifications

App Name: notes_app

#### Views:

- Notes Dashboard:
  - URL: GET /notes/
  - Template: notes/index.html
  - Description: Displays a user's notes list. Provides the option to create new notes and lists shared notes.
- Note Details:
  - URL: GET /notes/<int:note_id>/
  - Template: notes/note_details.html
  - Description: Displays the details about a specific note. Provides a link to the page that allows the user to edit a note.
- Create Note:
  - URL: POST /notes/create/
  - Template: notes/create_note.html
  - Description: Allows users to create a new note with a title and content.
- Edit Note:
  - URL: /notes/edit/<int:note_id>/
  - Function: edit_note(request, note_id)
  - Template: notes/edit_note.html
  - Description: Allows users to edit the content of a note.

#### Models:

Model: Note

The Note model is used to store information about the notes created by users. Each note has the following attributes:

- Title: A short title that describes the content of the note.
- Content: The main text or body of the note.
- Date Created: The date and time when the note was initially created.
- Last Modified: The date and time when the note was last edited.

### Getting Started

Your team needs to elect a `git manager` who will be responsible for creating the `upstream` repo and merging in pull requests.

#### Git Manager: Setting Up Upstream

1. **Create the Repository:**
   - Log in to your GitHub account.
   - Click the "+" button at the top right corner and select "New Repository."
   - Name the repository, choose visibility settings, and create the repository.
2. **Clone the Repository:**
   - Clone the repository to your local machine using `git clone <repository-url>`.
3. **Create Upstream Remote:**
   - In the terminal, navigate to the cloned repository's directory.
   - Add the original repository as an upstream remote using `git remote add upstream <original-repo-url>`.
4. **Push to Origin:**
   - Generate the initial code (Django project) in your local repository.
   - Commit and push the code to your repository's `main` branch using:
     ```
     git add .
     git commit -m "Initial commit"
     git push origin main
     ```
5. Merge in PRs
   - When a collaborator informs you that they have opened up a PR merge it on github and inform your group that there are changes ready to be pulled down.
   - To pull the changes to your local machine, run the following:
   ```
   # commit your work on your feature branch
   git add .
   git commit -m 'your commit message'
   # checkout to main
   git checkout main
   # download and merge new code
   git pull origin main
   # combine the code with your feature branch
   git checkout feature-branch
   git merge main
   ```
6. When submitting your own commits:
   - Option 1: Commit and push your changes to your fork's `feature-branch` branch using:
   ```
   git add .
   git commit -m "Commit message"
   git push origin feature-branch
   ```
   - Follow the steps from 5.
   - Option 2: Merge locally
   ```
    git add .
    git commit -m "Commit message"
    git checkout main
    git merge feature-branch
    git push origin main
   ```
   - inform your group that you have pushed new changes on to upstream.
   -

#### Collaborators: Forking and Setting Upstream

1. **Fork the Repository:**
   - Log in to your GitHub account.
   - Go to the Git manager's repository on GitHub. (They can slack you a link to it once it has been setup).
   - Click the "Fork" button in the top right corner. This will create a copy of the repository in your GitHub account.
2. **Clone Your Fork:**
   - Clone your forked repository to your local machine using `git clone <your-fork-url>`.
3. **Add Upstream Remote:**
   - In the terminal, navigate to the cloned repository's directory.
   - Add the Git manager's repository as an upstream remote using `git remote add upstream <original-repo-url>`.
4. **Stay in Sync with Upstream:**
   - Periodically fetch and merge the changes from the Git manager's repository to stay up to date:
     - If you are on a feature branch (you should be), run the following to get it up-to-date:
     ```
     # commit your work on your feature branch
     git add .
     git commit -m 'your commit message'
     # checkout to main
     git checkout main
     # download and merge new code
     git pull upstream main
     # push new code to your origin
     git push origin main
     # return to your feature branch
     git checkout feature-branch
     # merge in new code
     git merge main
     ```
     - If you have a rebase conflict when pulling from `upstream` on your `main` branch:
     ```
     # find out what is going on
     git status
     # if this is in fact a rebase with conflicts, run
     git rebase --abort
     # download code
     git fetch upstream
     # start merge conflict
     git merge upstream/main
     # communicate with your group about the merge conflit and resolve it with paired coding
     git add .
     git commit -m 'fixes merge conflict'
     # push fixed code to origin
     git push origin main
     # integrate new code with your feature branch
     git checkout feature-branch
     git merge main
     ```
5. **Collaborate on the App:**
   - Create, edit, and share notes through the app as per the lab activity's requirements -- communicate what everyone is working on and divy up the tasks.
   - Commit and push your changes to your fork's `feature-branch` branch using:
     ```
     git add .
     git commit -m "Commit message"
     git push origin feature-branch
     ```
   - open a PR on github and inform your git manager that there is code waiting to be merged.

## Resources

