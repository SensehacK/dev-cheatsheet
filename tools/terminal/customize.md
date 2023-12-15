# Customize

### Installation

Just use “OhMyZsh” tool to create a great terminal experience for everyday usage. It is terminal on steroids and it well maintained by the community.

[https://github.com/ohmyzsh/ohmyzsh](https://github.com/ohmyzsh/ohmyzsh)

#### Plugins

Auto Suggestions plugin [https://github.com/zsh-users/zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)

While running the command it automatically changes the color depending on whether the command is correct. [https://github.com/zsh-users/zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)

History auto complete plugin
https://superuser.com/questions/417627/oh-my-zsh-history-completion


Sometimes the plugins were not behaving properly or loading properly.
So explicitly sourced its shell script.
```bash
source ~/.oh-my-zsh/custom/plugins/zsh-autocomplete/zsh-autocomplete.plugin.zsh
```

This appeared to be a problem when working with external themes like [Powerlevel10K plugin thread issue](https://github.com/romkatv/powerlevel10k/issues/1631)
