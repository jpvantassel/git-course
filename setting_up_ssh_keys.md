# Git Basics

> Joseph P. Vantassel, The University of Texas at Austin

[![License](https://img.shields.io/badge/license-CC--By--SA--4.0-brightgreen.svg)](https://github.com/jpvantassel/git-course/blob/master/Licence.md)

## Setting up SSH keys (Stop Git from asking for my password)

Tired of typing your password? ... Set up an SSH key.

```bash
ls -al ~/.ssh                  # Check for existing SSH keys
```

You may see some defaults, such as:

* id_dsa.pub
* id_ecdsa.pub
* id_ed25519.pub
* id_rsa.pub

You can either use one of these (if they exist) or _generate a new SSH key_

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@email.com"   # Generates a new key, using the provided email
```

Enter a file in which to save the key

Enter passphrase - A passphrase enables an additional level of security, if your system is compromised. You will need to enter this passphrase every time you work with Git.

Add the key to the ssh-agent

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/<newkeyname>
```

Add key to GitHub account [follow this](https://help.github.com/en/articles/adding-a-new-ssh-key-to-your-github-account).

You may also need to _switch from HTTPS to SSH_ for this to work:

```bash
git remote -v
# This will show the current remotes (you will see HTTPS or SSH)
  # HTTPS look like: https://github.com/<USERNAME>/<REPO>.git
  # SSH look like: git@github.com:<USERNAME>/<REPO>.git
git remote set-url origin git@github.com:<USERNAME>/<REPO>.git   # You will get the SSH from the remote's page
git remote -v                                                    # Should see the updated remotes
```

## Sources

[Why is Git always asking for my password?](https://help.github.com/en/articles/why-is-git-always-asking-for-my-password)
