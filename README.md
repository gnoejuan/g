# g

Simple go version manager, gluten-free.

[![license](https://img.shields.io/github/license/stefanmaric/g.svg)](./LICENSE)

<div align="center"><img src="screencast.gif" alt="screencast"></div>

## Why?

Existing version managers build go from source, have too many dependencies, pollute the PATH, and/or require you to use a specific shell environment. `g` aims to be as unobtrusive and portable as possible.

`g` is inspired by [tj/n](https://github.com/tj/n) - which I have contributed to in the past - and borrows some of its code.


## Features

* Works no matter what shell you're using as long as `$GOPATH` and `$GOROOT` are exported, which are not specific to `g` but idiomatic to `go`.
* No need to `source` functions in your shell config.
* Single bash script that ideally lives where your go binaries live.
* Downloads pre-built binaries so it is fast and...
* ...requires no git, no mercurial, no gcc, no xcode, etc.
* `curl` and `wget` first-class support alike.
* Colorful UI and interactive but safe to pipe and use in automated scripts.


## Requirements

* macOS, Linux or BSD environment - should work just fine on [Bash for Windows (WSL)](https://docs.microsoft.com/en-us/windows/wsl/about).
* Bash 3+, check with `bash --version`
* Either [`curl`](https://en.wikipedia.org/wiki/CURL) **or** [`wget`](https://en.wikipedia.org/wiki/Wget), check with `curl -V` or `wget -V` respectively.

Not strictly necessary, but highly recommended, to completely remove any previous go installation — just to prevent any weird outcome.


## Install

### Single line

**IMPORTANT**: Before you continue, I encourage you to [read the install script](https://git.io/g-install); never trust someone telling you to run random commands.

That said, you can install `g` with a single command:

```shell
curl -sSL https://git.io/g-install | bash
```

If you use `wget` instead:

```shell
wget -qO- https://git.io/g-install | bash
```

That will download the [`g` script](./bin/g), put it inside `$GOPATH/bin/`, give it execution rights with `chmod`, and configure your default shell's initialization file, setting the `GOPATH` & `GOROOT` environment variables and adding `$GOPATH/bin` to the `PATH`.

**NOTE**: You must restart your current shell session for it to read these new env vars in order to use `g`. Alternatively, you can source your shell's init file, usually with the `source` command, but that will depend on the specific shell you use. For example, if you use `zsh`:

```shell
source ~/.zshrc
```

#### Shell support

The install script currently supports the following shells:

* bash
* zsh
* fish

The install script is going to select your default shell for configuration. You might see what your default shell is by running:

```shell
echo $SHELL
```

If you wish to configure a diff shell, you might pass it as arguments:

```shell
curl -sSL https://git.io/g-install | bash -s -- fish
```

You might as well configure several shells, but that's usually not required:

```
curl -sSL https://git.io/g-install | bash -s -- fish bash zsh
```

#### Changing defaults

By default, these go environment variables are used:

```
GOROOT: $HOME/.go
GOPATH: $HOME/go
```

`$GOPATH/bin` is added to the `PATH` and there's where `g` is copied to.

You might set those variables before running the install script. For example, in bash and zsh:

```shell
export GOROOT=~/.local/share/golang
export GOPATH=~/MyProjects/go-projects
curl -sSL https://git.io/g-install | bash
```

In fish:

```shell
set -gx GOROOT ~/.local/share/golang
set -gx GOPATH ~/MyProjects/go-projects
curl -sSL https://git.io/g-install | bash
```

### Manually

1. Make sure to export the `$GOPATH` & `$GOROOT` environment variables and add `$GOPATH/bin` to your `PATH`.
2. Grab a copy of the [`./bin/g`](./bin/g) script and put it anywhere available in your `PATH` — inside `$GOPATH/bin/` is a good option.
3. Give the script execution rights with `chmod +x $GOPATH/bin/g`.
4. Restart your shell session to make sure the env variables are loaded.


## Usage

```
  Usage: g [COMMAND] [options] [args]

  Commands:

    g                           Open interactive UI with installed versions
    g install <version>         Install go <version>
    g install latest            Install or activate the latest go release
    g install -a 386 latest     Force 32 bit architecture
    g install -o darwin latest  Override operating system
    g run <version>             Run a given version of go
    g which <version>           Output bin path for <version>
    g remove <version ...>      Remove the given version(s)
    g prune                     Remove all versions except the current version
    g list                      Output installed go versions
    g list-all                  Output all available go versions
    g help                      Display help information, same as g --help

  Options:

    -h, --help              Display help information and exit
    -v, --version           Output current version of g and exit
    -q, --quiet             Disable curl output (if available)
    -d, --download          Download only
    -c, --no-color          Force disabled color output
    -y, --non-interactive   Prevent prompts
    -o, --os                Override operating system
    -a, --arch              Override system architecture
```


## TODO

- [x] Improve docs
    - [ ] Improve a bit more
- [x] Install script
    - [ ] Add support for more shells
    - [ ] Add interactive multi-select UI to select shells
    - [ ] Add non-interactive mode
- [ ] Update script
- [ ] Improve the --quiet and --non-interactive modifiers
- [ ] Test it on diff platforms
- [ ] Write some tests


## The alternatives

* https://github.com/moovweb/gvm
* https://github.com/kennyp/asdf-golang
* https://github.com/hit9/oo
* https://github.com/andrewkroh/gvm


## Contributing

Please read [CONTRIBUTING.md](./CONTRIBUTING.md). ♥


## Acknowledgments

* [Every contributor to this project](https://github.com/stefanmaric/g/graphs/contributors).
* The [`n` project](https://github.com/tj/n), which  `g` is inspired by and based on.
* The [`n-install` project](https://github.com/mklement0/n-install), which `g` is also based on.


## License

[MIT](./LICENSE) ♥
