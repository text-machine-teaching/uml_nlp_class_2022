# Welcome Guide

Hello newcomer!

<Welcome message>
If you have any troubles or questions, do not hesitate to ask anybody.
We are interested in your progress just as you are and glad to help.

---

## Lab networking
We use [Slack](https://text-machine-test.slack.com/), Telegram and [Google group](https://groups.google.com/forum/#!aboutgroup/text-machine) for communication.
Subscribe to the google group and ask Vlad or Olga to add you to Slack.

Our GitHub: [github.com/text-machine-lab/](https://github.com/text-machine-lab)

> Slack can be tricky, and you should not expect it to notify everyone about each of your messages.
This is not a bug; this is a feature to respect your work-life balance.
To force-notify the lab, you can write "@everyone" in #general or to force-notify a channel, you can write "@channel".
E.g., "@everyone, my paper just got accepted to EMNLP!"

We have regular(-ish) meetings on Tuesday at 4 pm where we discuss papers and the work done this week.
Follow text-machine google group and #reading_club channel for updates.


## How to connect to servers

First, you should ask Vlad or Olga for an account.
If you are not familiar with ssh, read [this](https://www.digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys).
After that, add to your `.ssh/config` the following:

```
 Host cs
         User <YOUR_CS_USERNAME>
         HostName cs.uml.edu
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

> If your session keep being disconnected every hour, add `ServerAliveInterval 120` to `Host cs`

## Git and a project template

**Always** use git for your projects. `git init` should be the first thing you type in your new project.
This is a [project template](https://github.com/Guitaricet/ml-project-template) that can be useful for you.
Just click "use this template," and it will create a GitHub repository for you. It already has `.gitignore` and common recommendations.

Most research projects are poorly structured, but you can be better than the most.

## Code style

Read this post: [Nine simple steps for better-looking python code](https://towardsdatascience.com/nine-simple-steps-for-better-looking-python-code-87e5d9d3b1cf)

* First, remember that you write code to read it, not only to run it. And the worse project is written, harder it is to continue it after a few months.
* Use python>=3.6, we are way past 2015.
* Please, use a linter (we recommend flake8 for VS Code and default linter for PyCharm) for your code
and (roughly) follow [PEP 8](https://www.python.org/dev/peps/pep-0008).
* 4 spaces considered a standard indentation in the community and most text editors and IDE when you press tab), please follow it.
* Single quotes are preferred over double-quotes for strings.
* [F-strings](https://realpython.com/python-f-strings/) are preferred over (and a lot simpler)
[%-formatting](https://realpython.com/python-f-strings/#option-1-formatting)
and [str.format()](https://realpython.com/python-f-strings/#option-2-strformat)
* For docstrings, we recommend using reST or Google or Numpy [standard](https://stackoverflow.com/questions/3898572/what-is-the-standard-python-docstring-format). in the community and most text editors and IDE when you press tab), please follow it.
* Single quotes are preferred over double-quotes for strings.
* [F-strings](https://realpython.com/python-f-strings/) are preferred over (and a lot simpler)
[%-formatting](https://realpython.com/python-f-strings/#option-1-formatting)
and [str.format()](https://realpython.com/python-f-strings/#option-2-strformat)
* For docstrings, we recommend using reST or Google or Numpy [standard](https://stackoverflow.com/questions/3898572/what-is-the-standard-python-docstring-format).


## GPU usage

Please be respectful to others and always check which GPUs are currently used before running your model.

To check the usage of GPUs type the following command: `nvtop`

If it does not work, use `nvidia-smi` (and contact Vlad about this problem)

To select GPU, set CUDA_VISIBLE_DEVICES environment variable. For example, if you want to use GPUs number 0 and 2, run
`export CUDA_VISIBLE_DEVICES=0,2`

**Note:** For some weird and unknown reasons, Ishkur GPU enumeration is 1,0,2 (corresponding to GPU numbers in nvidia-smi and nvtop). 

## PyCharm guide

Most members of our lab use [PyCharm](https://www.jetbrains.com/pycharm/) as their main IDE. It has a lot of perks for Python development. The Community version is free, and the Professional version is [free for students](https://www.jetbrains.com/student/). PyCharm has some cool features like jupyter notebook support, scientific view, and version control; however, it is memory-consuming and can be slower than the alternatives. If you want more lightweight (but still very powerfull) text editor, we recommend [Visual Studio Code](https://code.visualstudio.com/).

### Using remote interpreters
We will set up PyCharm deployment, which is a tool that automatically updates your work on the server as you type in your IDE (like a Google doc). To do this:

1. Create a new project in PyCharm. Give it a pretty name. I recommend opening in a new window if given the option (PyCharm is annoying to use with multiple projects in one).
1. Set up Automatic Deployment:
    1. Make sure the project root is selected in the Project Toolbar (toggle toolbar with alt-1)
    1. In the menu bar, go to Tools -> Deployment -> Configuration
    1. In the top left, there is a “+” button. Click this to add a configuration. Name it.
    1. Under the ‘Connection’ tab that appears, select SFTP for ‘Type’ and fill in your server address and authentication details. After, hit ‘Autodetect’ and check that it correctly puts your home directory under the root path. Select ‘Save Password’ if you don’t want to log in every time.
    1. Under the ‘Mappings’ tab, you need to fill in the project path on your local machine, and the equivalent path on the server. For ‘Local path’, give it the path to the main folder on your local machine. For the deployment path, give it the path to the (currently empty) project folder, and keep in mind that your home directory is the root. For example, if the ‘Connections’ tab had “/home/arum” set as the root, then you would now use “/projects/my-project” to indicate the full path.
    1. Hit ‘OK’ to go back to your project.
    1. In the menu bar, check off  Tools -> Deployment -> Automatic Upload. This updates the files on the server every time you type. Try it out, and make sure it works.
    1. If you change the files on the server, it will not automatically download. With the project root selected, you must go to Tools -> Deployment -> Sync with Deployed, and choose what to do with each file. Use arrow keys to select a file, space-bar to switch actions, and enter key to apply the action.
1.  Set up remote execution environment
    1. Now that your project has been uploaded to the server, you need to create a virtual environment with the needed dependencies; then we can set up PyCharm to remotely execute your code from your local machine.
    1. Open a terminal window and ssh into the server (e.g. $ ssh shala_proxy )
    1. Create a directory for your virtual environments, and inside that make a directory for this project’s venv.
    1. Execute “virtualenv -p python3 directory_path” where “directory_path” is the one you just created. Most of our projects use python3, but if you need to replace that with a different version.
    1. To operate in the virtual environment, execute “source directory_path/bin/activate”. You’ll see the virtual environment name to the left of your current line. You can exit at any time by executing “deactivate”
    1. While in your venv, you can use “pip install package_name” to install packages that your code depends on, without affecting the rest of the system or other projects. You need to do this to set up all of your project dependencies
        1. Check the root folder of your project. If there is a file “requirements.txt”, you can execute “pip install -r requirements.txt” to set them all up.
        1. If there is no such file, ask the sages who worked on the project before you what dependencies you need so you can do it one go.
        1. Else, go through the torture of trying to run the code and installing the dependency associated with each error. Good luck.
1. Set up local execution on the remote system
    1. Pycharm has a cool feature where you can execute code on the server from within the IDE on your local computer. Go to File -> Settings 
    1. To the right of the “Project Interpreter” box, click on the gear, then click “add remote.”
    1. For Deployment config, select the server that you entered in step 3. For the python interpreter path, navigate to the bin folder in your virtualenv directory and select ‘python’. Hit OK. Hit OK on the other window too.
    1. You should now be able to execute your code on the server by hitting the play button in the top right of the IDE window.
    
## VS Code Guide

VS Code is faster than PyCharm, consumes ~5 times less memory, and supports all the features you need via extensions. 

1. [Install VS Code](https://code.visualstudio.com/)
1. Install the official [Python extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python)
1. Type `>python: select linter` and select flake8. VS Code can ask you to install it, answer yes.
1. Install [Remote Development](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack) extension to work directly on our GPU servers (it is much simpler to setup compared to PyCharm btw)

To use Remote Development:
1. Update your `.ssh/config` if you still haven't (see the instructions above)
1. In VS Code command line (`CMD + P` on Mac OS) type `>remote-ssh:connect to host`
1. A list of available connections should appear, select the one you need
1. You may need to install Python extension, and flake8 on your server as well
1. Select your project directory

More about [python development](https://code.visualstudio.com/docs/languages/python) and [remote development](https://code.visualstudio.com/docs/remote/remote-overview) using VS Code.


## Essential papers

Of course, this is not an exhaustive list of papers you need to know, but it covers the main approaches that we use in NLP today. Start reading these after you cover the basics.

We suggest reading the papers in the following order:

1. [Universal Language Model Fine-tuning for Text Classification](https://arxiv.org/abs/1801.06146), Howard and Ruder, 2018
    * The paper that introduced a ubiquitous by now fine-tuning paradigm to NLP
    * It has a lot of extra hipster hacks, but they are good to know
1. [Effective Approaches to Attention-based Neural Machine Translation](https://arxiv.org/abs/1508.04025), Luong et al. [Stanford], 2015
    * This is not the first paper on attention, but it has a clear explanation of attention mechanism
1. [Attention Is All You Need](https://arxiv.org/abs/1706.03762), Vaswani et al. [Google], 2017
    * **NOTE:** this paper is hard to read, while the concept is relatively simple; read this [excellent blog post](http://jalammar.github.io/illustrated-transformer/) instead and return to the paper later (or skip the paper entirely)
1. [BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding](https://arxiv.org/abs/1810.04805), Devlin et al. [Google], 2018
    * NLP working horse since 2018, there are a lot of newer models that outperform BERT, but they mostly build upon this one
    * Some alternative approaches: [GPT](https://openai.com/blog/language-unsupervised/), [RoBERTa](https://arxiv.org/abs/1907.11692), [ULM](https://arxiv.org/abs/1905.03197)


## Reproducibility

ML experiments may be very hard to reproduce. You have a lot of hyperparameters, different dataset splits, different ways to preprocess your data, bugs, etc.
Ideally, you should log data split (already preprocessed), all hyperparameters (including learning rate scheduling), the initial state of your model and optimizer, random seeds used for initialization, dataset shuffling and all of your code. Your GPU is also should be in deterministic mode (which is not the default mode). **For every single model run**. This is a very hard task. Different random seed can significantly [change your metrics](https://arxiv.org/abs/2002.06305) and even GPU-induced randomness can be important. We're not solving all of these problems, but we need to address at least what we can handle.

For every result you report in the paper you need (at least) to:
1. Track your model and optimizer hyperparameters (including learning rate schedule)
1. Save final model parameters
1. Report all of the parameters in the paper (make a table in the appendix) and release the code
1. [Set random seeds](https://github.com/catalyst-team/catalyst/blob/f909e5b44eb4c2c26039e201bcbe67001529a515/catalyst/utils/seed.py)
(it is not as easy as `torch.manual_seed(42)`, follow the link).
1. Store everything in the cloud

To save your hyperparameters you can use the TensorBoard HParams plugin, but we recommend using a specialized service like [wandb.ai](https://app.wandb.ai). These services not only store all of your logs but provide an easy interface to store hyperparameters, code and model files.

Ideally, also:
1. Save the exact code you used (create a tag in your repository for each run)
1. Save your preprocessed data,
especially if you are working on a dataset paper
([Data Version Control](https://dvc.org/) helps)
1. Save your model and optimizer initialization (the state at step 0)
1. Use GPU in deterministic mode (this will slightly affect the performance)
1. Store everything in the cloud **and** locally


An easy way to do this:
```python
# Before the training:
import random
import wandb
import torch
import numpy as np

random.seed(args.seed)     # python random generator
np.random.seed(args.seed)  # numpy random generator

torch.manual_seed(args.seed)
torch.cuda.manual_seed_all(args.seed)

torch.backends.cudnn.deterministic = True
torch.backends.cudnn.benchmark = False

wandb.init(..., config=args)  # keep all your hyperparameters in args
# wandb also saves your code files and git repository automatically

checkpoint = {
    'model': model.state_dict(),
    'optimizer': optimizer.state_dict(),
    'settings': args,
    'epoch': epoch,
    'step': global_step
}

torch.save(checkpoint, save_path_for_init)
wandb.save(save_path_for_init)  # upload your initialization to wandb

# Your training loop is here

# After the training:
checkpoint = {
    'model': model.state_dict(),
    'optimizer': optimizer.state_dict(),
    'settings': args,
    'epoch': epoch,
    'step': global_step
}

torch.save(checkpoint, save_path)
wandb.save(save_path)  # upload your trained model to wandb
```

### TL;DR

At least keep all your hyperparameters for every run.
Use specialized tools like
[wandb.ai](https://app.wandb.ai) or
[tensorboard.dev](https://tensorboard.dev/) + TensorBoard HParams for this.
Store them in the cloud, not on our local servers / your machine.


### Additional readings
  * [PyTorch docs on reproducibility](https://pytorch.org/docs/stable/notes/randomness.html)
  * [Fully reproducible research paper example](https://github.com/ibab/fully-reproducible)
  * [Independently Reproducible Machine Learning](https://thegradient.pub/independently-reproducible-machine-learning)
