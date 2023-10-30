# Commitizen

## Git Standard

Conventional commit messages as a global utility

### Installation

Install commitizen globally, if you have not already.

```sh
npm install -g commitizen
```


Install your preferred commitizen adapter globally, for example cz-conventional-changelog

```sh
npm install -g cz-conventional-changelog
```


### Configuration

Create a .czrc file in your home directory, with path referring to the preferred, globally installed, commitizen adapter

```sh echo '{ "path": "cz-conventional-changelog" }' &gt; ~/.czrc
```


Or you can open .czrc file and use

```config
{ "path": "cz-conventional-changelog" }
```

[Git commitment Repo ](https://github.com/commitizen/cz-cli#making-your-repo-commitizen-friendly)

