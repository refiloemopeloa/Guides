# A guide to using Node.js

Node.js is a JavaScript runtime environment that lets you create servers, web apps, command line tools and scripts. Basically, Node.js allows you to do a lot more with JavaScript.

## Setup

Setting up Node.js is quite easy. Here, I'll show you how to set it up on Windows, Linux, and macOS.

### Windows

Node.js has a pre-built installer, which you can find here: [Node.js — Download Node.js® (nodejs.org)](https://nodejs.org/en/download/prebuilt-installer)

### Linux

There are a few ways to do it on Linux, but we'll be using the Node Version Manager:

```shell
# installs nvm (Node Version Manager)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.0/install.sh | bash

# download and install Node.js (you may need to restart the terminal)
nvm install 20

# verifies the right Node.js version is in the environment
node -v # should print `v20.18.0` - this may change depending on the version you want to use

# verifies the right npm version is in the environment
npm -v # should print `10.8.2` - this may change, just as long as the printed version is this or higher
```

### macOS

macOS also has a prebuilt installer: [Node.js — Download Node.js® (nodejs.org)](https://nodejs.org/en/download/prebuilt-installer)

However, I find that using Brew is much easier:

```shell
# NOTE:
# Homebrew is not a Node.js package manager.
# Please ensure it is already installed on your system.
# Follow official instructions at https://brew.sh/
# Homebrew only supports installing major Node.js versions and might not support the latest Node.js version from the 20 release line.

# download and install Node.js
brew install node@20

# verifies the right Node.js version is in the environment
node -v # should print `v20.18.0`

# verifies the right npm version is in the environment
npm -v # should print `10.8.2` - this may change, just as long as the printed version is this or higher
```
