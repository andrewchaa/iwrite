# Migrating all my writings to Github pages

Github page uses Jekyll which is based on Ruby. I only have the default installation of ruby, so updated the version.

```bash
brew upgrade ruby
```

For some reason, it didn't succeed. I had to run a couple of more commands. It complained that `homebrew-core` and `homebrew-case` are shallow clones

```bash
git -C /usr/local/Homebrew/Library/Taps/homebrew/homebrew-cask fetch --unshallow
git -C /usr/local/Homebrew/Library/Taps/homebrew/homebrew-cask fetch --unshallow
```

