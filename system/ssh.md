# SSH

- [Connecting to GitHub with SSHw](https://help.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh)
- [How to set up ssh so you aren't asked for a password](https://www.debian.org/devel/passwordlessssh)

## Multiple SSH Keys settings for different + account

`~/.ssh/config`

```sh
Host github.com/abstractmagicalwand
        HostName github.com
        User git
        IdentityFile ~/.ssh/amv-work

Host github.com/captify-akrivchun
        HostName github.com
        User git
        IdentityFile ~/.ssh/captify-work
```

- [SSH Config file](https://www.ssh.com/ssh/config/)
- [Using Multiple SSH Public Keys](https://superuser.com/questions/272465/using-multiple-ssh-public-keys/272613#272613)
