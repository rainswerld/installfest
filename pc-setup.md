# Windows PC Installfest

Follow these instructions, along with an instructor, to install all of the software and tools we use during SEI on your Windows PC. **Some of these steps are complicated and will require you to work slowly and deliberately. Do not move on to the next step until your instructor has asked you to.**

There will be a few differences between your experince as a Windows user and the experiences of devs using Mac or Ubuntu. Most of these differences will be minor, but a few will be considerable and should be taken note of. As these come up during the course, please remember to refer back to this document as a reference.

## Initial Setup

1. Our first step will be installing [Git for Windows](https://gitforwindows.org/), which will allow us to, unsurprisingly, use git on Windows! Follow that link and download **Git for Windows**. Once downloaded, run the installer and follow the onscreen instructions **with the help of your instructor.**

2. Next, we will install the code editor you will be using throughout SEI, [Atom](https://atom.io/). Download the installer from that link and run it to install Atom.

3. If you haven't done so already, go to [GitHub](http://www.github.com) and create
an account; be sure to write down your username and password somewhere, since
we'll be using these credentials later. Next, go to [GitHub Enterprise](https://git.generalassemb.ly) and create an account. It is recommended that you use the same username. This will be the source of your learning material throughout SEI, while your personal Github will be where you showcase your projects.

4. We will now run a sequence of commands in our Git for Windows terminal (we'll just call the **the terminal** from now on). Make sure to copy these commands exactly and to run them one at a time!
    ```bash
    git config --global user.name "<username>"
    # replace <username> with your github/git enterprise username
    git config --global user.email "<email>"
    # replace <email> with your github/git enterprise email
    git config --global color.ui true
    git config --global pull.rebase true
    git config --global branch.autosetuprebase always
    git config --global push.default simple
    git config --global branch.autosetupmerge true
    git config --global core.editor "atom --wait"

    # set global gitignore file as ~/.gitignore
    git config --global core.excludesfile ~/.gitignore
    # copy .gitignore from this directory to home directory
    cp .gitignore ~/.gitignore

    # generate new ssh key and add it
    # the -t flag specifies the type of key
    # the -f flag specifies the path
    # the -N flag specifies a passphrase, blank in this case
    # the -C flag adds a comment to help identify the SSH key
    ssh-keygen -t rsa -f ~/.ssh/id_rsa -N '' -C "<email>"
    # replace <email> with your github/git enterprise email
    ssh-add ~/.ssh/id_rsa
    ```
5. Once those commands have been successfully run, we're going to run a couple more.
    ```bash
    # move to the .ssh folder 
    cd ~/.ssh/
    # opens the id_rsa file with Atom
    atom id_rsa.pub
    ```
    Once the file opens, you'll see a long string of numbers and letters that starts with `ssh-rsa` and ends with your email address. This is your ssh key. Copy the whole thing!

6.  Next, log into GitHub.com, go to [https://github.com/settings/ssh](https://github.com/settings/ssh)

7. Click the `New SSH key` button at the top right of the page

8. Enter a title for your SSH key (you can call it whatever you want)

9. Paste in your SSH key!

10. Click the `Add SSH key` button

11. In your terminal, run this command
    ```bash
    ssh -T git@github.com
    ```

    If you get a prompt along the lines of

    ```bash
    The authenticity of host 'github.com (xxx.xxx.xxx.xxx)'... can\'t be established.
    RSA key fingerprint is XX:XX:XX:XX:XX:XX:XX:XX:XX:XX:XX:XX:XX:XX:XX:XX:XX:XX.
    Are you sure you want to continue connecting (yes/no)?
    ```

    Just type 'yes'. If everything's working, you should get a response like the following:

    ```bash
    Hi <your_username>! You\'ve successfully authenticated, but GitHub does not provide shell access.
    ```

12.   Next, log into git.generalassemb.ly, go to [https://git.generalassemb.ly/settings/keys](https://git.generalassemb.ly/settings/keys), and paste in the same SSH key.

13. You've now finished the initial setup! Great work!

## Python Setup

Now we'll install the [Python](https://www.python.org/downloads/release/python-377/) language onto your computer. We will also be installing a package that will help us install other Python things called `pip`. 

1. Follow the above link, scroll to the *Files* section, and download the `Windows x86-64 executable installer`.

2. Run the installer with your instructor, making sure to click the *Add Python 3.x to PATH* checkbox.

3. Run this command in your terminal to install some of the tools we will be using with Python.
    ```sh
    pip3 install pipenv pylint
    ```

3. Finally, we will be creating an alias (kind of like a nickname for a command) for running Python. Git for Windows does not like to open Python the way we'd like it to, so we're going to create a file (.bashrc) and add a line to it to tell our terminal exactly how to run Python from now on. Run these commands in your terminal:
    ```sh
    cd ~

    touch .bashrc

    atom .bashrc
    ```

4. Next paste in the following, making sure to replace `<user>` with your Windows user.
    ```sh
    alias py="C:/Users/<user>/AppData/Local/Programs/Python/Python37/python.exe -i"  
    ```

5. Close and reopen your terminal.
    >**Note: Our friends using Mac and Ubuntu will use the command `python3` to run the Python shell. We will be using the command `py` to do the same thing.**

## Important Libraries

Next we're going to be installing two very important libraries that work alongside some of the tools we've already installed. `Libsass` and `tidy-html` will give us access to functinality we did not have previously.

### Libsass

Installing `libsass` is the easier of the two, so we'll start there.

1. Run the following command in your terminal:
    ```sh
    pip install libsass
    ```
2. You're finished!

### Tidy-html

Installing `tidy-html` is going to be a bit more involved than `libsass` and we're going to have to use a couple tools that we probably won't be using for the rest of the course.

The first is PowerShell, a special Windows terminal. The second is a package installer, called [Chocolatey](https://chocolatey.org/) that runs inside PowerShell. Let's get started.

1. First, type `powershell` in the Windows search bar and right click on PowerShell and select `Run as Administrator`.

2. Run the following command in PowerShell:
    ```sh
    # this command allows us to install programs via PowerShell
    Set-ExecutionPolicy Bypass -Scope Process
    ```
3. Next we will run another command in PowerShell to install Chocolatey. Make sure to copy and paste this exactly how it is.
    ```sh
    Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
    ```
4. Once the install finishes, we will run one last command to install `tidy-html`:
    ```sh
    choco install html-tidy
    ```
5. When that is done, close PowerShell and then close and reopen your terminal.

## Node Setup

We're going to be installing Node. Node (and its various packages) will be the foundation of a large part of the course.

### NVM (Node Version Manager)

First, we're going to install a tool called [NVM for Windows](https://github.com/coreybutler/nvm-windows#node-version-manager-nvm-for-windows) that allows us to maintain multiple different versions of Node, in case we want to switch between them for different projects. The original NVM is only available for Mac/Linux, this is an alternative with the same functionality.

1. Follow the above link and click *Download Now*. Under the heading 1.1.7 - Maintenance Release download nvm-setup.zip.

2. Unzip the file and run the installer with the instructor.

3. Next run these commands, one at a time, in the terminal.
    ```sh
    # installs a specific version of node
    nvm install 10.15.0
    # sets that version as the default
    nvm use 10.15.0
    ```
4. Close and reopen your terminal.

### NPM Packages
Now, we will use Node's associated package manager, `npm`, to download and install some Node modules and make them available across all of our projects.

Run this command in your terminal.
```sh
npm install --global jsonlint eslint grunt-cli remark-lint phantomjs-prebuilt nodemon node-sass
```

Once that is finished running, the Node setup is complete!

## PostgreSQL Setup

We will be installing PostgreSQL, an open source relational database management system. In SEI, we will be writing SQL (structured query language) and maintaining our relational databases using Postgres.

On Windows we will be following [this tutorial](https://medium.com/@itayperry91/get-started-with-postgresql-on-windows-a-juniors-life-4adfa6dd10e) to setup Postgres.

## MongoDB Setup

We'll now install MongoDB, another open source database. To do so, we will follow the install steps [here](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/).

Once those have been completed we will follow the steps [here](https://teamtreehouse.com/community/how-to-setup-mongodb-on-windows-cmd-or-gitbash-with-shortcuts) to set up MongoDB to work with our terminal.

# Congratulations, you have finished Installfest!