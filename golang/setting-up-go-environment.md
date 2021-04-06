# Setting up Go environment

Not the game of Go but golang

Go programs are organised into packages. 

* Package: a collection of source files in the same directory
* Module: a collection of related Go packages. 
* Repository: contains one or more modules

### Install Go

```bash
brew update && brew install golang
```

### Setup Workspace

It’s considered best practice to use `$HOME/go` location for your workspace, so let’s do that!

```text
mkdir -p $HOME/go/{bin,src,pkg}
```

### [Setup Environment](https://jimkang.medium.com/install-go-on-mac-with-homebrew-5fa421fc55f5)

We’ll need to add to `.bashrc` or `.zshrc` \(if you’re using zsh\) with the following info. \(Ex: `code ~/.zshrc` \)

```text
export GOPATH=$HOME/go
export GOROOT="$(brew --prefix golang)/libexec"
export PATH="$PATH:${GOPATH}/bin:${GOROOT}/bin"
```

## Setting up VS Code

Install Go extension. Either Microsoft or Google

Then with `shft + cmd + p`, Install / Update Go tools

![](../.gitbook/assets/image%20%2829%29.png)



