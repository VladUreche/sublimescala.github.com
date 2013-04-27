# Hacker Guide

This is a small guide on hacking the Ensime package for Sublime Text 2. If you find any inconsistencies or would like to
improve the documentation, please [visit the Ensime github page](https://github.com/sublimescala/sublimescala.github.com)
or file a bug at the [github issue tracker](https://github.com/sublimescala/sublimescala.github.com/issues/new). Thank you!

## Picking a Bug
There are many reasons to hack the Ensime plugin:
 * you would like to implement a feature
 * you may either have a bug that is anoying you every day
 * or maybe you just want to help out, may
other users of the Ensime plugin.

Either way, the first place to go to is the [the github issue tracker](https://github.com/sublimescala/sublime-ensime/issues?state=open): first look at the issues and improvement requests posted there, since it's likely your
feature of bug is already there. If not, feel free to [create a new issue](https://github.com/sublimescala/sublime-ensime/issues/new). If you're looking for something to work on, the [the critical bugs](https://github.com/sublimescala/sublime-ensime/issues?labels=critical&state=open) are probably the most useful to fix, if you care to spend some time on them.
Finally, once you identified and created the bug, it is best to announce you'll be working on a issue, so leave a comment saying so.

Okay, now you know what you'll be working on, so let's get hacking!

## Forking the Repo

Usually the best way to get your code in the repository by making [pull requests](https://help.github.com/articles/using-pull-requests). To do so, you will need to follow these steps:
1. Start by forking [the sublime-ensime repository](https://github.com/sublimescala/sublime-ensime)
2. Clone the repository on your machine, instead of the plugin installed automatically, and create a branch
3. Setup your environment
4. Start hacking on the plugin
5. When you're done, commit your changes and make a pull request in the github interface (or using [the hub script](https://github.com/defunkt/hub)).

This guide will detail steps 2 to 4, which should be the difficult parts. For steps 1 and 5, please refer to [the pull requests article on github](https://help.github.com/articles/using-pull-requests).

### Clone the Repository

You probably have the sublime-ensime plugin already installed on your machine, either manually or via Package Control. You will have to change your repository, so that you point it to your fork. To do so, start a terminal and change the directory to the plugin location (on Linux, that's `$HOME/.config/sublime-text-2/Packages/Ensime`):

If you installed via Package Control, you will not have any repository installed:
```bash
you@your-machine:~/.config/sublime-text-2/Packages/Ensime$ git remote -v
fatal: Not a git repository (or any of the parent directories): .git
you@your-machine:~/.config/sublime-text-2/Packages/Ensime$ git clone git@github.com:YourGithubUsername/sublime-ensime.git Bogus
Cloning into 'Bogus'...
...
you@your-machine:~/.config/sublime-text-2/Packages/Ensime$ mv Bogus/.git . # UGLY HACK, is there a better way?
you@your-machine:~/.config/sublime-text-2/Packages/Ensime$ rm -rf Bogus/
you@your-machine:~/.config/sublime-text-2/Packages/Ensime$ git branch issue/XX
you@your-machine:~/.config/sublime-text-2/Packages/Ensime$ git checkout issue/XX
Switched to branch 'issue/XX'
you@your-machine:~/.config/sublime-text-2/Packages/Ensime$ git push origin issue/XX
Total 0 (delta 0), reused 0 (delta 0)
To git@github.com:YourGithubUsername/sublime-ensime.git
 + 7f69aac...8533c16 issue/XX -> issue/XX
```

If you cloned the official repo, you will have it installed already:
```bash
you@your-machine:~/.config/sublime-text-2/Packages/Ensime$ git remote -v
you@your-machine:~/.config/sublime-text-2/Packages/Ensime$ git remote -v
origin  git://github.com/sublimescala/sublime-ensime.git (fetch)
origin  git://github.com/sublimescala/sublime-ensime.git (push)
you@your-machine:~/.config/sublime-text-2/Packages/Ensime$ git remote rename origin trunk
you@your-machine:~/.config/sublime-text-2/Packages/Ensime$ git remote add origin git@github.com:YourGithubUsername/sublime-ensime.git
you@your-machine:~/.config/sublime-text-2/Packages/Ensime$ git fetch origin
...
you@your-machine:~/.config/sublime-text-2/Packages/Ensime$ git branch issue/XX
you@your-machine:~/.config/sublime-text-2/Packages/Ensime$ git checkout issue/XX
Switched to branch 'issue/XX'
you@your-machine:~/.config/sublime-text-2/Packages/Ensime$ git push origin issue/XX
Total 0 (delta 0), reused 0 (delta 0)
To git@github.com:YourGithubUsername/sublime-ensime.git
 + 7f69aac...8533c16 issue/XX -> issue/XX
```

Now you have branch `issue/XX` and you can start hacking on it!

### Setup your Environment

The typical setup includes a Scala project you prepared and adding the `Ensime` directory to the project. To do so, start
by creating a directory and put Scala sources inside it. Use the `Command Palette` to start Ensime. Typically, you should
try to reproduce the problem in your project.

To further help with reproducing the problem, we'll briefly explain the internal architecture of the `sublime-ensime` plugin.

#### Internals, take 1: Overview

The plugin consists of two main pieces:
 * the [sublime-ensime plugin itself](https://github.com/sublimescala/sublime-ensime), which queries the ensime engine.
 * the [ENSIME server](https://github.com/aemoncannon/ensime), which runs an incremental Scala compiler, the same which is used in the [Scala IDE for Eclipse](http://scala-ide.org/).

These two components communicate back an forth with queries and commands, with the sublime plugin starting and querying the ensime server to display errors, autocompletions and perform other useful work

When hacking the plugin, you probably won't need to patch the ensime server but the sublime-ensime plugin itself, which is written in Python. Nevertheless, you will surely need to understand the communication that goes on between the sublime plugin and the ensime server. For this, you need to skim through the [ENSIME User Manual](http://aemoncannon.github.io/ensime/index.html). Note that ENSIME started out as a Scala plugin for EMACS, thus inherits the communication protocol from there.

Now, how to see the debug output for these two components, bring up the `Command Palette` and look for `Ensime: Client Log` for the plugin log and `Ensime: Server Log` for the `ENSIME` log.

### Start Hacking the Plugin
TODO

#### Internals, take 2: Plugin
TODO


Happy hacking!
The SublimeScala team.