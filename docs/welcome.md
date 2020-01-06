# Welcome Guide

Hello newcomer! \<Welcome message>

If you have any troubles or questions, do not hesitate to ask anybody.
We are interested in your progress just as you are and glad to help.

## Lab networking
We use [Slack](https://text-machine-test.slack.com/), Telegram and [Google group](https://groups.google.com/forum/#!aboutgroup/text-machine) for communication.
Subscribe to the google group and ask Vlad or Olga to add you to Slack.

Our GitHub: [github.com/text-machine-lab/](https://github.com/text-machine-lab)

## How to connect to servers

First, you should ask Vlad or Olga for account.
If you are not familiar with ssh, read [this](https://www.digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys).
After that, add to your `.ssh/config` the following:

```
 Host cs
         User <YOUR_CS_USERNAME>
         HostName cs.uml.edu
         ServerAliveInterval 120 # a hack to bypass session length limit
 Host enki
         User <YOUR_USERNAME>
         HostName 172.16.33.13
         ProxyJump cs
 Host ishkur
         User <YOUR_USERNAME>
         HostName 172.16.33.14
         ProxyJump cs
 Host inanna
         User <YOUR_USERNAME>
         HostName 172.16.33.17
         ProxyJump cs
 Host shala
         User <YOUR_USERNAME>
         HostName 172.16.33.15
         ProxyJump cs
 Host marduk
         User <YOUR_USERNAME>
         HostName 172.16.33.9
         ProxyJump cs
 Host dumuzi
         User <YOUR_USERNAME>
         HostName dumuzi.cs.uml.edu
         ProxyJump cs
 ```

It will allow you to connect to a server via `ssh enki` (no username or connection to cs is needed)
and to use VS Code Remote or PyCharm remote easily.
But first, you need to copy your `ssh id` to a server you plan to use. E.g.,

```bash
ssh-copy-id enki
```

It would allow you to connect to the server without typing your password.

## Git and project template

**Always** use git for your projects. `git init` should be the first thing you type in your new project.
This is a [project template](https://github.com/Guitaricet/ml-project-template) that can be useful for you.
Just click "use this template" and it will create GitHub repository for you. It already has `.gitignore` and common recommendations.

Most of research projects are poorly structured, but you can be better that the most.

## Code style

* First, remember that you write code to read it, not only to run it. And worse the project is written, harder to return to it after a few months.
* Use python>=3.6, we are way past 2015.
* Please, use a linter (we recommend flake8 for VS Code and default linter for PyCharm) for your code
and (roughly) follow [PEP 8](https://www.python.org/dev/peps/pep-0008).
* 4 spaces considered a standard indentation> How to connect to servers and where to seek help

---

Hello newcomer!

<Welcome message>
If you have any troubles or questions, do not hesitate to ask anybody.
We are interested in your progress just as you are and glad to help.

## Lab networking
We use [Slack](https://text-machine-test.slack.com/), Telegram and [Google group](https://groups.google.com/forum/#!aboutgroup/text-machine) for communication.
Subscribe to the google group and ask Vlad or Olga to add you to Slack.

Our GitHub: [github.com/text-machine-lab/](https://github.com/text-machine-lab)

## How to connect to servers

First, you should ask Vlad or Olga for an account.
If you are not familiar with ssh, read [this](https://www.digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys).
After that, add to your `.ssh/config` the following:

```
 Host cs
         User <YOUR_CS_USERNAME>
         HostName cs.uml.edu
         ServerAliveInterval 120 # a hack to bypass session length limit
 Host enki
         User <YOUR_USERNAME>
         HostName 172.16.33.13
         ProxyJump cs
 Host ishkur
         User <YOUR_USERNAME>
         HostName 172.16.33.14
         ProxyJump cs
 Host inanna
         User <YOUR_USERNAME>
         HostName 172.16.33.17
         ProxyJump cs
 Host shala
         User <YOUR_USERNAME>
         HostName 172.16.33.15
         ProxyJump cs
 Host marduk
         User <YOUR_USERNAME>
         HostName 172.16.33.9
         ProxyJump cs
 Host dumuzi
         User <YOUR_USERNAME>
         HostName dumuzi.cs.uml.edu
         ProxyJump cs
 ```

It will allow you to connect to a server via `ssh enki` (no username or connection to cs is needed)
and to use VS Code Remote or PyCharm remote easily.
But first, you need to copy your `ssh id` to a server you plan to use. E.g.,

```bash
ssh-copy-id enki
```

It would allow you to connect to the server without typing your password.

## Git and a project template

**Always** use git for your projects. `git init` should be the first thing you type in your new project.
This is a [project template](https://github.com/Guitaricet/ml-project-template) that can be useful for you.
Just click "use this template" and it will create a GitHub repository for you. It already has `.gitignore` and common recommendations.

Most research projects are poorly structured, but you can be better than the most.

## Code style

* First, remember that you write code to read it, not only to run it. And the worse project is written, harder it is to continue it after a few months.
* Use python>=3.6, we are way past 2015.
* Please, use a linter (we recommend flake8 for VS Code and default linter for PyCharm) for your code
and (roughly) follow [PEP 8](https://www.python.org/dev/peps/pep-0008).
* 4 spaces considered a standard indentation in the community and most text editors and IDE when you press tab), please follow it.
* Single quotes are preferred over double-quotes for strings.
* [F-strings](https://realpython.com/python-f-strings/) are preferred over (and a lot simpler)
[%-formatting](https://realpython.com/python-f-strings/#option-1-formatting)
and [str.format()](https://realpython.com/python-f-strings/#option-2-strformat)
* For docstrings, we recommend using reST or Google or Numpy [standard](https://stackoverflow.com/questions/3898572/what-is-the-standard-python-docstring-format). in the community and in most text editors and IDE when you press tab), please follow it.
* Single quotes are preferred over double quotes for strings.
* [F-strings](https://realpython.com/python-f-strings/) are preferred over (and a lot simpler)
[%-formatting](https://realpython.com/python-f-strings/#option-1-formatting)
and [str.format()](https://realpython.com/python-f-strings/#option-2-strformat)
* For docstrings, we recommend to use reST or Google or Numpy [standard](https://stackoverflow.com/questions/3898572/what-is-the-standard-python-docstring-format).
