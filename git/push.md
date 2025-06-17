
## no verify

You may need to disable pre commit hooks git hooks sometimes in order quickly push through something.


```sh
	git push origin --no-verify
```

--no-verify works, but in my case, I didn't want to put the parameter all the time on the terminal. So I opted for something a little more aggressive.


Disable 
locally globally

```sh
git config core.hooksPath /dev/null  
git config --global --unset core.hooksPath
```

Enable
```sh
git config --global --unset core.hooksPath  
```

[SO thread](https://stackoverflow.com/questions/7230820/skip-git-commit-hooks)

If you want to disable git hooks globally, you could try running this:

git config --global core.hooksPath /dev/null  
But, if you want to leave it as it was before, just run the following command in your terminal:

git config --global --unset core.hooksPath  
If you do not want it to be global, just remove the argument: --global

[github desktop thread](https://github.com/desktop/desktop/issues/11626)