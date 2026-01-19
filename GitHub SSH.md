#GitHub #SSH 
# SSH on GitHub

(Source: [Setting Up SSH Keys for GitHub - YouTube](https://www.youtube.com/watch?v=8X4u9sca3Io&list=LL&index=75&t=545s))

To do any operation on GitHub require a ssh key, you will need a way to identify as yourself. This is the easiest way to do it.

## 1. Generate ssh key

Type following in terminal

```bash
ssh-keygen -t ed25519 -C your_github_mail@gmail.com
```

System will return some option, for our personal use, they can be skipped.(If need for higher security, further research must be done)

## 2. Check ssh-agent

```bash
eval "$(ssh-agent -s)"
```

This will check if ssh-agent exits. It's like a vault that will store our info.

## 3. Add private key to the ssh-agent

First, we need to crate the config file is exist

```bash
~/.ssh/config
```

If not exist (most of the time, it not there), we need to create it by ourselves

```bash
nvim ~/.ssh/config
```

Input following into the config file

```
Host *
        AddKeysToAgent yes
        IdentityFile ~/.ssh/id_ed25519
```

Finally, we can add ssh-key to our ssh-agent

```bash
ssh-add ~/.ssh/id_ed25519
```

## 4. Setting on the GitHub

1. Go to GitHub, and go to "setting" > "SSH and GPG keys"
2. Create New ssh keys, also check if there are any unknown or not using ssh keys
3. Get the public key with following

```
cat ~/.ssh/id_ed25519.pub
```

## 5. Test the ssh key

If everything is right, ssh should be working now. Just in case, we should still test it. 

```bash
ssh -T git@github.com
```

The return should be

```bash
Hi {your_username}! You've successfully authenticated, but GitHub does not provide shell access.
```

If so, the ssh key is create successfully, and the work is done!
