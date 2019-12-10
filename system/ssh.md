# SSH

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
