# Contributing

Thanks for your interest in contributing! Please read carefully through our
guidelines below to ensure that your contribution adheres to our project's
standards.

## Issue Tracking

We use
[GitHub Issues](https://github.com/xFuture603/homelab-hardening-guide/issues)
to track all tasks related to this project.

## Contribute your changes

There are three steps to set up a working environment:

1. [Fork the repository](#fork-the-repository)
2. [Clone your fork](#clone-your-fork)
3. [Add your changes](#add-your-changes)

### Fork the repo

A _fork_ is a copy of a repository. Forking a repository lets you to make
changes to your copy without affecting any of the original code.

Click **Fork** (in the top-right corner of the page) to copy this repository
to your GitHub account.

### Clone your fork

A _clone_ is a downloaded version of a repository. Cloning our fork lets you
download a copy of the repository to your computer.

Use `git clone` to clone your fork

```
$ git clone https://github.com/xFuture603/homelab-hardening-guide.git
```

### Add your changes

If you followed the steps from above, you now have the repo on your computer.
Now go into the repository folder and add your changes.

For example, if you are working in the `~/dev` directory:

```
cd ~/dev

vim /file/you/want/to/change

save your changes
```

## Submit a Pull Request

Remember how making changes on a _fork_ doesn't affect the original code?
Well, in order to fix an issue in the main project,
you _want_ to change the original code. A _pull request_
is a GitHub feature that lets you do just that!

There are three steps to submitting a pull request:

- [Contributing](#contributing)
  - [Issue Tracking](#issue-tracking)
  - [Contribute your changes](#contribute-your-changes)
    - [Fork the repo](#fork-the-repo)
    - [Clone your fork](#clone-your-fork)
    - [Add your changes](#add-your-changes)
  - [Submit a Pull Request](#submit-a-pull-request)
    - [Save your changes locally](#save-your-changes-locally)
    - [Send your changes to your fork](#send-your-changes-to-your-fork)
    - [Open a Pull Request](#open-a-pull-request)
  - [License](#license)

### Save your changes locally

First, get a list of all the files you have changed.

```
$ git status
```

Next, _stage_ the file you want to save. This will add the file to a new list
that is ready to be saved.

```
$ git add /files/you/changed
```

Save your staged files. For example:

```
$ git commit -m "docs: added section for segmented vlan"
```

### Send your changes to your fork

Use the `git push` command to add your local made changes to your remote fork

```
$ git push origin main
```

### Open a Pull Request

1. Find the [Create Pull Request](https://github.com/xFuture603/homelab-hardening-guide/compare/) button
1. Select **compare across forks**
1. Add your forked branch and select the right base repository
1. Click **Create Pull Request**

## License

By contributing, you agree that your contributions will be licensed under its
Attribution-ShareAlike 4.0 International license.
