# macos-pyenv-binary

![.github/workflows/build.yml](https://github.com/youngminz/pyenv-macos-binary/workflows/.github/workflows/build.yml/badge.svg)

After upgrading macOS to Big Sur, Python build using pyenv did not work properly, such as readline library not being compiled. Thankfully, GitHub allows me to build code and upload artifacts on macOS Catalina.

How to use: Download the desired Python version artifact from GitHub Action and unzip it to ~/.pyenv/versions to complete the installation.

When compiling Python, the Python installation path is hardcoded into the Hashbang(#!) or various configuration files. After unzipping, edit the hardcoded files to match your username with the shell script below. 

```bash
cd ~/.pyenv/versions

# For some reason, you have to use two below commands to make a complete change.
LC_CTYPE=C LANG=C find ./ -type f -exec sed -i -e "s|/Users/runner/|${HOME}/|g" {} \;
grep -rl '/Users/runner' . | LC_CTYPE=C LANG=C xargs sed -i '' -e "s|/Users/runner/|${HOME}/|g"

# Make sure everything has replaced.
grep -rnw . -e '/Users/runner'
```
