# GitHub Actions Workflow Setup

## Overview

This workflow automatically compiles LaTeX CVs and deploys them to the public `cv-repo`.

## Architecture

- **applications-repo** (private) - Contains LaTeX source files
- **cv-repo** (public) - Receives compiled PDFs only

## Setup Instructions

### 1. Create Personal Access Token

1. Go to GitHub Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Click "Generate new token (classic)"
3. Configure:
   - **Note**: `CV Repo Deploy Token`
   - **Expiration**: No expiration (or set based on preference)
   - **Scopes**:
     - `repo` (Full control of private repositories)
4. Click "Generate token" and copy it immediately

### 2. Add Token to Repository Secret

1. Go to applications-repo → Settings → Secrets and variables → Actions
2. Click "New repository secret"
3. Configure:
   - **Name**: `CV_REPO_TOKEN`
   - **Value**: Paste the personal access token from step 1
4. Click "Add secret"

### 3. Workflow Triggers

The workflow runs when:
- Push to `main` branch modifies files in `curriculum_vitae/**/*.tex` or `curriculum_vitae/**/*.cls`
- Pull request to `main` (compiles but doesn't deploy)

### 4. What Happens

1. Checkout applications-repo source code
2. Compile `swe-resume.tex` using XeLaTeX
3. Compile `quant-resume.tex` using XeLaTeX
4. Checkout cv-repo (public)
5. Copy compiled PDFs to `cv-repo/docs/`
6. Commit and push PDFs to cv-repo

## Files Deployed

- `swe-resume.pdf` → `cv-repo/docs/swe-resume.pdf`
- `quant-resume.pdf` → `cv-repo/docs/quant-resume.pdf`

## Troubleshooting

### LaTeX Compilation Errors

Check the Actions log for LaTeX errors. Common issues:
- Missing packages
- Syntax errors in .tex files
- Font issues

### Push Failures

If the workflow can't push to cv-repo:
- Verify `CV_REPO_TOKEN` secret exists
- Verify token has `repo` scope
- Verify token hasn't expired
- Verify cv-repo repository exists

### Skip CI

Commits from the workflow include standard commit messages. To skip CI in cv-repo, the workflow would need to add `[skip ci]` to the commit message.
