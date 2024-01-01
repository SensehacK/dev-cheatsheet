

## Command

```sh
ssh username@10.0.0.11 -vvvvA
```

Providing `-vvvvA` will give you debug logs for ssh connection.


## Generate Key

[Generating a new SSH key and adding it to the ssh-agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)


## Adding Key

Adding a new SSH key to your Git Cloud hosted service
- [Github](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account) 


## Auto SSH

It is like a daemon to monitor the service / like a watchdog to restart the service if it crashes or stops abruptly.
[autossh restart](https://www.harding.motd.ca/autossh/)

 [Stack Exchange | How to reliably keep an SSH tunnel open?](https://superuser.com/questions/37738/how-to-reliably-keep-an-ssh-tunnel-open) 

## Errors

`kex_exchange_identification: Connection closed by remote host`
