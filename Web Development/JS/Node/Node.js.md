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

## Installing a package

You can install packages with `npm` that extend the functionality of `JavaScript`. This can be done by typing the following in your terminal:

```shell
npm install <package-name>
```

Running the command above creates a `node_modules` directory and a `package.json` file in the directory you ran the command above in. 

### node_modules

This folder is where the packages are installed.

### package.json

This file contains all the details about the packages you installed in that directory. This `package.json` is very useful when you are collaborating with other people, or when you are sharing your project because it allows the user to install any packages you installed in your project, without needing to know the package names. They can do this by running:

```shell
npm install
```

### Installation flags

Often you'll see more flags added to the `install` command:

- `--save-dev` 
	- installs and adds the entry to the `package.json` file `devDependencies`.
	- `devDependencies`: contains development tools, like a testing library.
- `--no-save` 
	- installs but does not add the entry to the `package.json` file `dependencies`.
	- `dependencies`: bundled with the app in production.
- `--save-optional` 
	- installs and adds the entry to the `package.json` file `optionalDependencies`
	- `optionalDependencies`: build failure of the dependency will not cause installation to fail.
- `--no-optional` 
	- will prevent optional dependencies from being installed.

Shorthand's of the flags can also be used:

- -S: `--save`
- -D: `--save-dev`
- -O: `--save-optional`

## Uninstalling packages

If you no longer need to use a package in your code, it is a good idea to  uninstall it and remove it from your project's dependencies. This is because packages tend to be quite large and tend to slow down the building of your project.

### Uninstalling local packages

#### Removing a local package from your node_modules directory

To remove a package from your `node_modules` directory, on the command line, use the `uninstall` command. Include the scope if the package is scoped. More on scopes later.

This uninstalls a package, completely removing everything `npm` installed on its behalf.

It also removes the package from the `dependencies`, `devDependencies`, `optionalDependencies`, and `peerDependencies` objects in your `package.json`.

Further, if you have an `npm-shrinkwrap.json` or `package-lock.json`, `npm` will update those files as well. More on these files later.

##### Unscoped package

`npm uninstall <package_name>`

##### Scoped package

`npm uninstall <@scope/package_name>`

###### Scopes

Scopes are basically just a way of grouping related packages together. Scopes allow you to create a package with the same name as a package created by another user without conflict. Read more on scopes [here](https://docs.npmjs.com/cli/v9/using-npm/scope).

#### Removing a local package without removing it from package.json

Using the `--no-save` will tell `npm` not to remove the package from your `package.json`, `npm-shrinkwrap.json`, or `package-lock.json` files. You may want to do this if you are not currently using a package but still want the people you are working with to be able to install it.

#### Confirming local package uninstallation

To confirm that `npm uninstall` worked correctly, check that the `node_modules` directory no longer contains a directory for the uninstalled package(s).

```shell
ls node_modules
```

#### Uninstalling global packages

You can uninstall global packages by using the `-g` flag after `uninstall`.

# References

1. [Node.js — Run JavaScript Everywhere (nodejs.org)](https://nodejs.org/en)
2. [Node.js — Download Node.js® (nodejs.org)](https://nodejs.org/en/download/package-manager)
3. [Node.js — An introduction to the npm package manager (nodejs.org)](https://nodejs.org/en/learn/getting-started/an-introduction-to-the-npm-package-manager)
4. [Uninstalling packages and dependencies | npm Docs (npmjs.com)](https://docs.npmjs.com/uninstalling-packages-and-dependencies)
5. [scope | npm Docs (npmjs.com)](https://docs.npmjs.com/cli/v9/using-npm/scope)