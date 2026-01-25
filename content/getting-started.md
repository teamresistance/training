---
title: "Getting Started with Development"
---

This guide will help you set up your development environment and begin working on the [programming challenges](/challenges/). By the end, you'll have your own local copy of our robot code template and be ready to start coding.

---

## What You'll Need

- A computer running Windows, macOS, or Linux
- Basic familiarity with using a terminal/command prompt
- A [GitHub account](https://github.com/signup) (free)

---

## Step 1: Introduction to Git and GitHub

### What is Git?

Git is a version control system that tracks changes to your code over time. It allows you to:

- Save snapshots of your work (commits)
- Work on new features without breaking existing code (branches)
- Collaborate with others without overwriting each other's changes
- Revert mistakes and see the history of your project

### What is GitHub?

GitHub is a website that hosts Git repositories online. It adds collaboration features like:

- Pull requests for code review
- Issue tracking for bugs and features
- Online code browsing and search
- Automated testing and deployment

### Learning Resources

If you're new to Git and GitHub, work through these tutorials first:

- [GitHub's Git Tutorial](https://docs.github.com/en/get-started/quickstart/set-up-git) - Official getting started guide
- [Git Handbook](https://docs.github.com/en/get-started/using-git/about-git) - Core Git concepts explained
- [GitHub Flow](https://docs.github.com/en/get-started/quickstart/github-flow) - How to use branches and pull requests

### Essential Git Commands

Here are the commands you'll use most often. Each command has both a **command-line** option and an **IDE** option using VS Code:

#### Clone a Repository

Download a repository to your computer.

**Command Line:**

```bash
git clone <repository-url>
```

**VS Code:**

1. Press **Ctrl+Shift+P** (Windows/Linux) or **Cmd+Shift+P** (macOS)
2. Type "Git: Clone" and press Enter
3. Paste the repository URL and choose a folder

---

#### Check Status

See which files have been modified.

**Command Line:**

```bash
git status
```

**VS Code:**

- The Source Control panel (sidebar icon with branches) shows modified files automatically
- Click the Source Control icon or press **Ctrl+Shift+G** / **Cmd+Shift+G**

---

#### Stage Files for Commit

Prepare files to be saved in the next commit.

**Command Line:**

```bash
git add <file-name>          # Add specific file
git add .                    # Add all changed files
```

**VS Code:**

1. Open the Source Control panel (**Ctrl+Shift+G** / **Cmd+Shift+G**)
2. Click the **+** icon next to individual files, or click **+** next to "Changes" to stage all

---

#### Commit Changes

Save a snapshot of your staged changes.

**Command Line:**

```bash
git commit -m "Description of changes"
```

**VS Code:**

1. Open the Source Control panel
2. Type your commit message in the text box at the top
3. Press **Ctrl+Enter** (Windows/Linux) or **Cmd+Enter** (macOS), or click the checkmark icon

---

#### Push to GitHub

Upload your commits to GitHub.

**Command Line:**

```bash
git push
```

**VS Code:**

1. Open the Source Control panel
2. Click the **...** menu → **Push**, or
3. Click **Sync Changes** if available at the bottom of the window

---

#### Pull from GitHub

Download the latest changes from GitHub.

**Command Line:**

```bash
git pull
```

**VS Code:**

1. Open the Source Control panel
2. Click the **...** menu → **Pull**, or
3. Click **Sync Changes** at the bottom of the window (pulls and pushes)

---

#### Create and Switch to a New Branch

Start working on a new feature or challenge.

**Command Line:**

```bash
git checkout -b <branch-name>
```

**VS Code:**

1. Click the branch name in the bottom-left corner of the window
2. Select **Create new branch...**
3. Enter the branch name and press Enter

---

#### Switch to an Existing Branch

Change to a different branch.

**Command Line:**

```bash
git checkout <branch-name>
```

**VS Code:**

1. Click the branch name in the bottom-left corner
2. Select the branch you want from the list

---

#### View Commit History

See past commits.

**Command Line:**

```bash
git log --oneline
```

**VS Code:**

1. Open the Source Control panel
2. Click the **...** menu → **View History** (requires Git Graph extension), or
3. Right-click a file and select **View File History**

---

## Step 2: Install the GitHub CLI

The GitHub CLI (`gh`) is a command-line tool that makes it easy to interact with GitHub. We'll use it to manage your development workflow.

### Installation Instructions

#### macOS

Using Homebrew (recommended):

```bash
brew install gh
```

#### Windows

Using winget:

```bash
winget install --id GitHub.cli
```

Or download the installer from [cli.github.com](https://cli.github.com/).

#### Linux

**Debian/Ubuntu:**

```bash
sudo apt install gh
```

**Fedora/RHEL:**

```bash
sudo dnf install gh
```

**Arch Linux:**

```bash
sudo pacman -S github-cli
```

### Authenticate with GitHub

After installation, authenticate the CLI with your GitHub account.

**Command Line:**

```bash
gh auth login
```

Follow the prompts to:

1. Choose "GitHub.com"
2. Select "HTTPS" as your preferred protocol, or "SSH" if you're comfortable with managing your own keys
3. Authenticate using your web browser

Verify it worked:

```bash
gh auth status
```

**VS Code:**

1. Open the Source Control panel (**Ctrl+Shift+G** / **Cmd+Shift+G**)
2. If not signed in, you'll see a **Sign in to GitHub** button
3. Click it and follow the browser authentication prompts
4. Look for your GitHub username in the bottom-left corner to confirm

---

## Step 3: Understanding the Drive Template

Team Resistance maintains a base robot code template at [teamresistance/Newbie_Gym](https://github.com/teamresistance/Newbie_Gym). This repository contains:

- **WPILib project structure** - Standard FRC robot code layout
- **AdvantageKit integration** - Logging framework for replay and debugging
- **Phoenix 6 configuration** - Motor controller libraries for CTRE devices
- **Swerve drive implementation** - Team 86's standard drivetrain code
- **Code quality tools** - Linters, formatters, and CI/CD configuration

### Why Use the Template?

For the [programming challenges](/challenges/), you'll be creating your own robot subsystems and commands. Rather than starting from scratch, you'll **clone** (download a copy of) the `Newbie_Gym` repository. This gives you:

- A working build system configured for FRC
- Team coding standards and best practices pre-configured
- Simulation support for testing without hardware
- The ability to practice Git workflows (branches, commits, pull requests)

You'll work in your local copy independently, and mentors can review your progress through your branches.

---

## Step 4: Clone the Template

### Clone the Repository

Download your local copy of the `Newbie_Gym`.

**Command Line:**

```bash
git clone https://github.com/teamresistance/Newbie_Gym.git
```

This command will clone the repository to your computer in a new `Newbie_Gym` folder.

**VS Code:**

1. Press **Ctrl+Shift+P** (Windows/Linux) or **Cmd+Shift+P** (macOS)
2. Type "Git: Clone" and press Enter
3. Enter the repository URL: `https://github.com/teamresistance/Newbie_Gym.git`
4. Choose a folder location on your computer

---

### Navigate to Your Project

**Command Line:**

```bash
cd Newbie_Gym
```

**VS Code:**

- If you just cloned: Click **Open** when prompted, or use **File → Open Folder** and select the `Newbie_Gym` folder

---

### Verify Your Setup

Check that your clone is properly connected.

**Command Line:**

```bash
git remote -v
```

**VS Code:**

1. Open the terminal in VS Code (**Terminal → New Terminal**)
2. Type `git remote -v` and press Enter

You should see `origin` pointing to the **Team Resistance repository** (`teamresistance/Newbie_Gym`).

---

## Step 5: Open the Project in VS Code

FRC development uses Visual Studio Code with the WPILib extension. If you haven't already:

1. Install [VS Code](https://code.visualstudio.com/)
2. Install the [WPILib suite](https://docs.wpilib.org/en/stable/docs/zero-to-robot/step-2/wpilib-setup.html) (includes Java, Gradle, and robot libraries)

Open your cloned project.

**Command Line:**

```bash
code .
```

**VS Code:**

- Launch VS Code and use **File → Open Folder** to select the `Newbie_Gym` directory

---

## Step 6: Build and Simulate

Before starting the challenges, verify the project builds and runs in simulation.

### Build the Project

In VS Code, press **Ctrl+Shift+P** (Windows/Linux) or **Cmd+Shift+P** (macOS) and type:

```bash
WPILib: Build Robot Code
```

The build should complete successfully. If you see errors, ask a mentor for help.

### Run Simulation

Press **Ctrl+Shift+P** / **Cmd+Shift+P** and type:

```bash
WPILib: Simulate Robot Code
```

Choose "Sim GUI" when prompted. The simulation window should open, and you can enable the robot. This confirms your development environment is working.

---

## Step 7: Start Your First Challenge

Now you're ready to begin! Head over to the [Programming Challenges](/challenges/) page and start with **Challenge 1: Command-Based Fundamentals**. You'll work in your local clone.

### Workflow for Each Challenge

As you work through challenges, follow this Git workflow. Each step shows both command-line and IDE options:

#### 1. Create a Branch for the Challenge

**Important Branch Naming:** Always include your first name at the beginning of your branch names (e.g., `john-challenge-1` or `sarah-challenge-1`). This helps mentors identify whose work they're reviewing.

**Important About main Branch:** The `main` branch is locked and you cannot merge changes into it. Instead, you'll build each new challenge branch off your previous challenge branch. For example:
- Challenge 1: Create `yourname-challenge-1` from `main`
- Challenge 2: Create `yourname-challenge-2` from `yourname-challenge-1`
- Challenge 3: Create `yourname-challenge-3` from `yourname-challenge-2`

This way, each challenge builds on your previous work.

**Command Line (for Challenge 1):**

```bash
git checkout -b yourname-challenge-1
```

Replace `yourname` with your actual first name (e.g., `git checkout -b john-challenge-1`).

**VS Code (for Challenge 1):**

1. Click the branch name in the bottom-left corner
2. Select **Create new branch...**
3. Type `yourname-challenge-1` (replace `yourname` with your first name) and press Enter

---

#### 2. Make Your Changes and Test Your Code

Write your code and test it in simulation!

---

#### 3. Stage and Commit Your Work

**Command Line:**

```bash
git add .
git commit -m "Complete Challenge 1: Command-based fundamentals"
```

**VS Code:**

1. Open the Source Control panel (**Ctrl+Shift+G** / **Cmd+Shift+G**)
2. Click **+** next to "Changes" to stage all files
3. Type your commit message: "Complete Challenge 1: Command-based fundamentals"
4. Press **Ctrl+Enter** / **Cmd+Enter** or click the checkmark

---

#### 4. Push to the Repository

**Command Line:**

```bash
git push -u origin yourname-challenge-1
```

Replace `yourname` with your actual first name.

**VS Code:**

1. Click **Sync Changes** at the bottom of the window, or
2. Open Source Control panel → **...** menu → **Push**
3. If prompted, confirm you want to publish the branch

---

#### 5. Create a Pull Request (for Mentor Review)

Create a pull request so mentors can review your work. **Note:** Your pull request will remain open for review only - it will not be merged into `main` since that branch is locked. This is just for feedback and code review.

**Command Line:**

```bash
gh pr create --title "[YourName] Challenge 1 Complete" --body "Completed command-based fundamentals challenge"
```

Replace `[YourName]` with your actual first name.

**VS Code / Web Browser:**

1. After pushing, VS Code may show a notification to **Create Pull Request** - click it, or
2. Visit the repository on GitHub (`github.com/teamresistance/Newbie_Gym`)
3. Click the **Compare & pull request** button that appears
4. Add title: "[YourName] Challenge 1 Complete" (replace with your first name)
5. Add description: "Completed command-based fundamentals challenge"
6. Click **Create pull request**

---

#### 6. After Mentor Review, Create Your Next Branch

Your mentor will review your PR and provide feedback. Once approved, you're ready for the next challenge!

**For the next challenge**, create a new branch **from your current challenge branch** (not from `main`):

**Command Line:**

```bash
git checkout yourname-challenge-1
git checkout -b yourname-challenge-2
```

**VS Code:**

1. Click the branch name in the bottom-left corner
2. Select your previous challenge branch (e.g., `yourname-challenge-1`)
3. Click the branch name again and select **Create new branch...**
4. Type your next challenge branch name (e.g., `yourname-challenge-2`)

This builds Challenge 2 on top of your Challenge 1 work. Repeat this process for each subsequent challenge.

---

## Getting Help

If you run into problems:

- **Build errors:** Ask a mentor to review your code
- **Git issues:** Check the [Git Handbook](https://docs.github.com/en/get-started/using-git/about-git) or ask for help
- **WPILib questions:** See [WPILib documentation](https://docs.wpilib.org/)
- **Team-specific questions:** Talk to programming mentors at meetings

---

## Next Steps

- [Start Challenge 1: Command-Based Fundamentals](/challenges/#challenge-1-command-based-fundamentals)
- Review [Code Standards](/standards/) to understand team conventions
- Explore [Subsystem IO Abstraction](/abstract-io/) patterns used in challenges
