

## Profiles

`.zshrc` or `.bashrc`


## History 

Changing history size

```sh
export HISTSIZE=10000
export HISTFILESIZE=10000
```


## What Shell

```sh
echo $SHELL
```

so our github actions CI runner uses bash shell and my personal machine has `zsh`

It seems I was not able to assign these values appropriately

`device` environment variable = iPhone-

```sh
{% raw %}
device: ${{ 'xcrun xctrace list devices 2>&1 | grep -oE ''iPhone.*?[^\(]+'' | head -1 | awk ''{$1=$1;print}'' | sed -e "s/ Simulator$//" ' }}
{% endraw %}
```

Zsh

```sh
built_device=`eval "$device"` 
# zsh: command not found: iPhone-

built_device=$device
# works
```

Bash
```sh
built_device=$device
echo $built_device
# prints the whole un-executed script `xcrun xctrace ... Simulators$//"`

built_device=`eval "$device"`
echo $built_device
# prints iPhone-
```