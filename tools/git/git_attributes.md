# Attributes

{% embed url="https://stackoverflow.com/questions/2517190/how-do-i-force-git-to-use-lf-instead-of-crlf-under-windows\#13154031" caption="Excellent thread in terms of proper standards." %}

Also we can utilize Git Attributes file in order to make sure we have consistent encoding set when working in cross platform environment.

{% embed url="https://www.richie-bendall.ml/gitattributes-generator/" caption="" %}



## Submodules

### Disable Dirty change set
Modified content dirty submodule.

```config

[submodule "subModule_name"]
	path = subModule_name
	url = ../path-subModule_name.git
	branch = master
	ignore = dirty

```

[SO](https://stackoverflow.com/questions/3240881/git-can-i-suppress-listing-of-modified-content-dirty-submodule-entries-in-sta)

[Ignore changes](https://medicineyeh.wordpress.com/2015/07/15/how-to-ignore-changes-in-git-submodules/)