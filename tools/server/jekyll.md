

## Errors

### Parser Issue

```log
Liquid Exception: Liquid syntax error (line 31): Variable '{{ 'xcrun xctrace list devices 2>&1 | grep -oE ''iPhone.*?[^\(]+'' | head -1 | awk ''{$1=$1;print}' was not properly terminated with regexp: /\}\}/ in tools/terminal/config.md
```

So for some reason it was parsing my code in escaped markdown format 
```
``` some code here ```
```

But was fixed by utilizing `raw` tags

```sh
{% raw %}
device: ${{ 'xcrun xctrace list devices 2>&1 | grep -oE ''iPhone.*?' }}
{% endraw %}
```
