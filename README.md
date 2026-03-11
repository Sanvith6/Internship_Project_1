# Internship Project 1

This repository is a sample submission for the DevOps intern task:

1. Learn basic Linux commands and Git workflow  
2. Create a Git repository and push a sample project  
3. Share the repository link in the group

## Project Overview

This project includes:
- A practice list of commonly used Linux commands
- A basic Git workflow for version control
- A sample shell script: `scripts/hello.sh`

## Repository Structure

```text
.
├── README.md
└── scripts
    └── hello.sh
```

## Linux Commands Practice

```bash
pwd
ls -la
cd <folder>
mkdir demo && cd demo
touch notes.txt
echo "Hello DevOps" > notes.txt
cat notes.txt
cp notes.txt notes-copy.txt
mv notes-copy.txt archive.txt
rm archive.txt
```

## Git Workflow

```bash
git init
git status
git add .
git commit -m "Initial commit: sample DevOps project"
git branch -M main
git remote add origin <your-repo-url>
git push -u origin main
```

## Run the Sample Project

On Linux/macOS:

```bash
chmod +x scripts/hello.sh
./scripts/hello.sh
```

Expected output:

```text
Hello from the DevOps sample project!
```

