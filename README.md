# Internship_Project_1

Learning basic Linux commands and Git workflow.

## DevOps Intern Task - Sample Project

This repository demonstrates:
- Basic Linux commands
- Basic Git workflow
- A sample project pushed to Git

## 1) Basic Linux Commands (Quick Practice)

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

## 2) Basic Git Workflow

```bash
git init
git status
git add .
git commit -m "Initial commit: sample DevOps project"
git branch -M main
git remote add origin <your-repo-url>
git push -u origin main
```

## 3) Sample Project

The sample project is a tiny shell script under `scripts/`:
- `scripts/hello.sh`

Run it on Linux:

```bash
chmod +x scripts/hello.sh
./scripts/hello.sh
```

Expected output:

```text
Hello from the DevOps sample project!
```

## 4) Share Repository Link

After pushing to GitHub/GitLab, share the repository URL in your group.

Example:

```text
https://github.com/<username>/devops-intern-sample
```
