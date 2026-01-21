---
title: "Getting Started with Development"
---

This guide will help you set up your development environment and begin working on the [programming challenges](/challenges/). By the end, you'll have your own fork of our robot code template and be ready to start coding.

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

Here are the commands you'll use most often:

```bash
# Clone a repository (download it to your computer)
git clone <repository-url>

# Check the status of your working directory
git status

# Stage files for commit (prepare them to be saved)
git add <file-name>          # Add specific file
git add .                    # Add all changed files

# Commit your changes (save a snapshot)
git commit -m "Description of changes"

# Push your commits to GitHub (upload)
git push

# Pull the latest changes from GitHub (download updates)
git pull

# Create and switch to a new branch
git checkout -b <branch-name>

# Switch to an existing branch
git checkout <branch-name>

# See your commit history
git log --oneline
```

---

## Step 2: Install the GitHub CLI

The GitHub CLI (`gh`) is a command-line tool that makes it easy to interact with GitHub. We'll use it to fork repositories and manage your development workflow.

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

After installation, authenticate the CLI with your GitHub account:

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

---

## Step 3: Understanding the Drive Template

Team Resistance maintains a base robot code template at [teamresistance/Drive_Template](https://github.com/teamresistance/Drive_Template). This repository contains:

- **WPILib project structure** - Standard FRC robot code layout
- **AdvantageKit integration** - Logging framework for replay and debugging
- **Phoenix 6 configuration** - Motor controller libraries for CTRE devices
- **Swerve drive implementation** - Team 86's standard drivetrain code
- **Code quality tools** - Linters, formatters, and CI/CD configuration

### Why Fork the Template?

For the [programming challenges](/challenges/), you'll be creating your own robot subsystems and commands. Rather than starting from scratch, you'll **fork** (make your own copy of) the `Drive_Template` repository. This gives you:

- A working build system configured for FRC
- Team coding standards and best practices pre-configured
- Simulation support for testing without hardware
- The ability to practice Git workflows (branches, commits, pull requests)

You'll work in your fork independently, and mentors can review your progress by looking at your repository on GitHub.

---

## Step 4: Fork and Clone the Template

### Fork the Repository

Create your personal copy of the `Drive_Template`:

```bash
gh repo fork teamresistance/Drive_Template --clone
```

This command will:

1. Create a fork under your GitHub account (e.g., `your-username/Drive_Template`)
2. Clone it to your computer in a new `Drive_Template` folder
3. Set up the original repository as an "upstream" remote (for pulling updates)

### Navigate to Your Project

```bash
cd Drive_Template
```

### Verify Your Setup

Check that your fork is properly connected:

```bash
git remote -v
```

You should see:

- `origin` pointing to **your fork** (`your-username/Drive_Template`)
- `upstream` pointing to the **original repository** (`teamresistance/Drive_Template`)

---

## Step 5: Open the Project in VS Code

FRC development uses Visual Studio Code with the WPILib extension. If you haven't already:

1. Install [VS Code](https://code.visualstudio.com/)
2. Install the [WPILib suite](https://docs.wpilib.org/en/stable/docs/zero-to-robot/step-2/wpilib-setup.html) (includes Java, Gradle, and robot libraries)

Open your cloned project:

```bash
code .
```

Or launch VS Code and use **File → Open Folder** to open the `Drive_Template` directory.

---

## Step 6: Build and Simulate

Before starting the challenges, verify the project builds and runs in simulation.

### Build the Project

In VS Code, press **Ctrl+Shift+P** (Windows/Linux) or **Cmd+Shift+P** (macOS) and type:

```
WPILib: Build Robot Code
```

The build should complete successfully. If you see errors, ask a mentor for help.

### Run Simulation

Press **Ctrl+Shift+P** / **Cmd+Shift+P** and type:

```
WPILib: Simulate Robot Code
```

Choose "Sim GUI" when prompted. The simulation window should open, and you can enable the robot. This confirms your development environment is working.

---

## Step 7: Start Your First Challenge

Now you're ready to begin! Head over to the [Programming Challenges](/challenges/) page and start with **Challenge 1: Command-Based Fundamentals**.

### Workflow for Each Challenge

As you work through challenges, follow this Git workflow:

1. **Create a branch for the challenge:**

   ```bash
   git checkout -b challenge-1
   ```

2. **Make your changes and test your code**

3. **Stage and commit your work:**

   ```bash
   git add .
   git commit -m "Complete Challenge 1: Command-based fundamentals"
   ```

4. **Push to your fork:**

   ```bash
   git push -u origin challenge-1
   ```

5. **Create a pull request** (optional, for mentor review):

   ```bash
   gh pr create --title "Challenge 1 Complete" --body "Completed command-based fundamentals challenge"
   ```

6. **After mentor approval, merge and move to the next challenge**

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
