---
title: "SSH connection issue"
date: 2023-03-25
# weight: 1
# aliases: ["/first"]
tags: ["ssh"]
author: "Orange"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: true
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
editPost:
    URL: "https://github.com/<path_to_repo>/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
math: true
type: post
---
I always encounter some ssh issue.
### Resource temporarily unavailable
One day...

```bash
> ssh -T git@github.com
ssh: connect to host ssh.github.com port 22: Resource temporarily unavailable
```

so there are several assumptions:
1. windows firewall block port 22
2. I do not generate ssh key for my github account
3. I do not configure my config file properly
4. SSH dies

I suggest following the steps below:
1. restart ssh

```bash
sudo service ssh restart
```

2. reinstall ssh

```bash
sudo apt-get remove openssh-server
sudo apt-get install openssh-server
```

3. generate ssh key for you github account

[generate ssh key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

[add key to your github account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

make configuration in `~/.ssh/config` file
```
Host github.com
Hostname ssh.github.com
User example@youremail
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa
Port 443

```

4. try `ssh -T git@github.com`