# macbook
Standard steps to configure mackbooks for club use
# 🧰 Code Club MacBook Setup: VS Code + GitHub (No Prompts)

This guide sets up Visual Studio Code with GitHub access using either a pre-generated Personal Access Token (PAT) or OAuth, ensuring learners can clone, commit, and push without authentication prompts.

---

## ✅ 1. Install Homebrew

Homebrew is the macOS package manager used to install Git, GitHub CLI, and VS Code.

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## ✅ 2. Install GitHub CLI and Git

These tools allow GitHub authentication and Git operations from the command line.
```bash
brew install gh git
```

## ✅ 3. Install Visual Studio Code

VS Code is the primary editor used by Code Club learners.

```bash
brew install --cask visual-studio-code
```

## ✅ 4. Install VS Code Extensions

These extensions support Python, GitHub, and beginner-friendly coding environments.

```bash
code --install-extension ms-python.python
code --install-extension ms-vscode.cpptools
code --install-extension github.vscode-pull-request-github
code --install-extension ms-vscode.gitlens
code --install-extension ms-toolsai.jupyter
```

## ✅ 5. Configure Git Identity and Credential Storage

Set the global Git identity and enable macOS Keychain to store credentials securely.

```bash
git config --global user.name "CodeClubUser"
git config --global user.email "lichfieldcodeclub@gmail.com"
git config --global credential.helper osxkeychain
```

## ✅ 6. Authenticate GitHub Access
Option A: Use a Pre-generated PAT (No MFA)

1. Trigger a Git operation:

```bash
git clone https://github.com/codeclub-org/welcome-repo.git
```

 2. When prompted:
   1. Username: codeclubuser
   2. Password: paste the PAT
3. Git stores this in macOS Keychain — no future prompts.

Option B: Use GitHub OAuth in VS Code
1. Open VS Code
2. Open Command Palette (Cmd+Shift+P)
3. Run: Git: Clone
4. Choose Clone from GitHub
5. Sign in via browser and authorize GitHub for VS Code
6. OAuth token is stored securely

## ✅ 7. Optional: Preload Credentials for Reproducibility

Use this only on managed machines. It stores credentials in plaintext.

```bash
git config --global credential.helper store
echo "https://codeclubuser:<PAT>@github.com" >> ~/.git-credentials
```

## ✅ 8. Suppress GitHub Extension Prompts (Optional)
If learners don’t need GitHub PR/issue features:
1. Open Extensions (Cmd+Shift+X)
2. Search for GitHub Pull Requests and Issues
3. Click Disable

## ✅ 9. Verify Git Configuration and Credential Storage
Check that Git is correctly configured and credentials are stored.

```bash
git config --list --show-origin
gh auth status
```

## ✅ 10. Create a Desktop Shortcut for First-Time Setup (Optional)
Create a shell script at ~/setup/gh-login:

```bash
#!/bin/bash
gh auth login --with-token < ~/setup/token.txt
```

Make it executable:

```bash
chmod +x ~/setup/gh-login

```
Create an AppleScript wrapper:

```Applescript
do shell script "/Users/codeclubuser/setup/gh-login"
```
Save as an Application in Script Editor → name it gh-login.app → place on Desktop.

## ✅ Double-clickable, no Terminal window, runs silently.


    
