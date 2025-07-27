# 1. Take care of safe directories
```bash
git config --global --add safe.directory /(directory)
```
*   This command tells Git that the specified directory is safe to operate in, even if its ownership is not strictly conventional.

## 2. Configure Git User Identity

Git requires a user name and email to associate with your commits.

```bash
git config --global user.name "username"
git config --global user.email "email"
```
* replace username with your actual username same with email
## 3. Switch Git Remote to SSH

Initially, your remote was set to HTTPS, which often requires repeated password/token entry. We switched to SSH for more secure and convenient authentication using SSH keys.

First, verify your current remote:
```bash
git remote -v
```

Then, set the remote URL to use SSH:
```bash
git remote set-url origin git@github.com:username/repo.git
```
*   Replace `username/repo.git` with your actual GitHub username and repository name if different.

## 4. Generate and Add SSH Key to GitHub

To authenticate with GitHub via SSH, you need an SSH key pair.

### a. Generate SSH Key

```bash
ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519 -q -N "" -C "email"
```
*   `-t ed25519`: Specifies the encryption algorithm (Ed25519 is recommended).
*   `-f ~/.ssh/id_ed25519`: Specifies the file path for the key (default location).
*   `-q`: Quiet mode (suppresses output).
*   `-N ""`: Sets an empty passphrase (for convenience; for higher security, use a passphrase).
*   `-C "email"`: Adds a comment to the key (usually your email).

### b. Get Public Key Content

```bash
cat ~/.ssh/id_ed25519.pub
```
*   Copy the **entire output** of this command.

### c. Add Public Key to GitHub

1.  Go to your GitHub account settings in a web browser.
2.  Navigate to "SSH and GPG keys".
3.  Click "New SSH key" or "Add SSH key".
4.  Provide a descriptive title.
5.  Paste the copied public key content into the "Key" field.
6.  Click "Add SSH key".

## 5. Add GitHub to Known Hosts

Sometimes, your SSH client might not recognize GitHub's host key, leading to "Host key verification failed" errors.

```bash
ssh-keyscan github.com >> ~/.ssh/known_hosts
```
*   This command fetches GitHub's SSH host key and appends it to your `~/.ssh/known_hosts` file, telling your SSH client to trust GitHub.

## 6. Push Changes to GitHub

After all the above steps, you can finally push your local commits to your GitHub repository.

```bash
git push
```
*   This command pushes the changes from your current branch to the remote repository.

