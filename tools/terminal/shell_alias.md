# Alias

### Git Alias

My favorite git commands with maximum 3 characters to save some time and frustration of repeating the command twice.

```text
alias gs='git status '
alias ga='git add '
alias gaa='git add -A '
alias gb='git branch '
alias gc='git commit '
alias gcm='git commit -m '
alias go='git checkout '
alias goo='git checkout master '
alias gss='git stash '
alias gsa='git stash apply '
alias grv='git remote -v '
alias gp='git push '
```

### Terminal

alias clr='cat /dev/null &gt; ~/.bash\_history && history -c && exit' alias ut="uptime" \# Computer uptime alias ip="curl icanhazip.com" \# Your public IP address

```bash
curl ipinfo.io/city
```

https://askubuntu.com/questions/673910/how-to-monitor-public-ip-and-the-locationcountry-state-city-simultaneously-i
### NPM

alias ni='npm install' alias ns='npm start' alias ibp='ionic build --prod'

### Ionic

alias icb='ionic cordova build ios --emulator' alias ib='ionic cordova build' alias ii='ionic info' alias is='ionic serve'

### Shorthand

#### App

alias textedit='open -a TextEdit’ alias o="open ." \# Open the current directory in Finder

#### Services

alias audioR="sudo kill -9 `ps ax|grep 'coreaudio[a-z]' | awk '{print $1}'`" alias ks='echo "$\_\_ksWelcome"'


#### Youtube DL

You can add this as an alias

`alias yt-dl='yt-dlp -f bestvideo+bestaudio'`