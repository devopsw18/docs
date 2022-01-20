---
sidebar_position: 1
sidebar_label: Setup GitLab SSH
---
# Carelyo GitLab

## Setup GitLab SSH

### Generate an SSH key pair
1. Open Terminal or GitBash for Windows or click to download for windows [Gitbash](https://gitforwindows.org)
2. In the Type 
```bash
ssh-keygen -t ed25519 -C "<comment>"
Replace <comment> with what you like.
```
3. Press enter. Output similar to the following is displayed:

```bash
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/user/.ssh/id_ed25519):
```
4. Accept the suggested filename and directory.
5. Specify a passphrase:

```bash
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
```
6. A confirmation is displayed, including information about where your files are stored.

### Add an SSH key to your GitLab account
1. Copy the contents of your public key file. You can do this manually or use a script. For example, to copy an ED25519 key to the clipboard:

macOS:

```bash
tr -d '\n' < ~/.ssh/id_ed25519.pub | pbcopy
```
Linux (requires the xclip package):

```bash
xclip -sel clip < ~/.ssh/id_ed25519.pub
```
2. Sign in to GitLab.
3. On the top bar, in the top right corner, select your avatar.
4. Select Preferences.
5. On the left sidebar, select SSH Keys.
6. In the Key box, paste the contents of your public key. If you manually copied the key, make sure you copy the entire key, which starts with ssh-ed25519 or ssh-rsa, and may end with a comment.
7. In the Title box, type a description, like Work Laptop or Home Workstation.
8. Select Add key.
