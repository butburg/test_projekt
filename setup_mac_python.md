# The right way to install Python on a Mac

>https://medium.com/marvelous-mlops/the-rightway-to-install-python-on-a-mac-f3146d9d9a32

## 1. Install XCode Command Line Tools

The first step is to install the command line tools for mac. This includes all kinds of useful stuff for developers, such as a C compiler. You can also use the app store to install it, but you’re a developer now. So we’ll be doing things from the command line in this tutorial.

```
xcode-select --install
```

## 2. Install HomeBrew

Next, install HomeBrew — the open source package manager for mac. Browse to https://brew.sh/ and copy and run the command at the top of the page. It should look something like:

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Note that HomeBrew does not automatically update itself nor any of the packages installed. Do this yourself once in a while by executing:

```
brew update
brew
```

## 3. Install Pyenv

Pyenv is a package manager specifically for python itself. It allows you to install multiple versions of python on one machine. The pyenv-virtualenv plugin helps create virtualenvs for a specific python version.

```
brew install pyenv pyenv-virtualenv
```

I’m a Z Shell (zsh) user, so this step is a bit specific. Why zsh over regular bash? Well, you can see a comparison here and decide for yourself. In short: more features. The drawback is that your commands locally can differ from the ones needed on your cloud deployments, where you might have to deal with just regular bash. But I digress
For this step below make sure you properly initalise pyenv and pyenv-virtualenv. In order to do this in zshell, place the following lines in .zshrc in your home directory.

```
eval "$(pyenv init -)"

if which pyenv-virtualenv-init > /dev/null; then eval "$(pyenv virtualenv-init -)"; fi
```

Next, restart all your terminals to ensure pyenv is initialized.

## 4. Install your desired version of python

Great, you now have pyenv + pyenv-virtualenv! Let’s get some python, no, let’s go crazy, let’s go all kinds of versions of python. Just because we can! But we’ll start with one. To see what’s on offer you can list all available python versions by running.

```
pyenv install -l
```

Note that the base versions (denoted by just a number) are listed at the top. Also note that newer versions only become available when you upgrade pyenv (see updating HomeBrew and its packages above).
Install your favorite version of python with the command below.

```
pyenv install 3.12.0
```

Substitute 3.12.0 for your desired version here of course. You can have multiple versions installed simultaneously by using this command. No worries mate!

## 5. Create a virtualenv

>*Personal Note:* start from here with VSCode to create and select virtualenv out of project

Change directory to the root of your project. Decide which version of python you want to use. Have a look at which version you have installed and are available to you.
pyenv versions
You should see the version or versions here that you chose to install. Next you can create a virtualenv with a version of choice. I usually have identical names for my projects, repositories and virtualenvs. I like to keep a clean 1 virtualenv per project / repository. This allows me to easily manage my dependencies.

```
pyenv virtualenv 3.12.0 myproject
```

This will create a virtualenv named “myproject” with python version 3.12.0. Next, activate the environment for your project by running.

```
pyenv local myproject
```

This will create a file named .python-version that contains the name of the virtualenv. Make sure to never commit this file to git! Now, your prompt should probably start with (myproject), unless you have configured your terminal in some funky customized way.

## Deleting environments

If you want to delete a python environment use the project name as an argument in the following code.
pyenv virtualenv-delete myproject

## Create requiremenst.txt

Simply run
```pip freeze > requirements.txt```

## Initialize git

Simply run
```git init -b main```
