# Setup Your Local Windows Environment

These instructions will help you setup a _Linux-Like_ terminal environment on your Windows machine to help you build and implement your _FullStack Application_ on the cloud.

## Download and Setup Git and your Git Bash Terminal

1. [Open the Git website](https://www.git-scm.com)

2. Click the **Download link** to [download Git](https://git-scm.com/download/win). The download should automatically start.

3. Once downloaded, start the installation from the browser or the download folder. If Windows prompts you for _User Account Control_, it will ask you the following:

-   **Do you want to allow this app to make changes to your device?**
-   **SELECT YES** and proceed with the following installation steps:

    -   [ ] In the _Git 2.2x.x.x Setup_ Dialog Box, _Git_ will present you with an **Information** screen that will ask you to read through their **Terms & Conditions** and/or **GNU General Public License**. Please read and scroll through them to proceed and **Click Next** to accept and continue the workflow.

    ![Step 1](https://github.com/New-Data-Company/SmartImport_Frontend/blob/master/public/wiki/GitForWindows/Step1.PNG)

    -   [ ] Next, the _Git_ Workflow will ask you to **Select Destination Location** for this new installation of _Git_ and **Git Bash** on your machine. The recommended location is acceptable and you can proceed and **Click Next** to continue. In this example we have left it at `C:\Program Files\Git` as shown in the image.

    ![Step 2](https://github.com/New-Data-Company/SmartImport_Frontend/blob/master/public/wiki/GitForWindows/Step2.PNG)

    -   [ ] In the **Select Components** window, leave all default options checked and check any other additional components you want installed and **Click Next**.

    ![Step 3](https://github.com/New-Data-Company/SmartImport_Frontend/blob/master/public/wiki/GitForWindows/Step3.PNG)

    -   [ ] **Select Start Menu Folder** and leave the name listed as the default option `Git` so we can access this from the Windows _Start Menu_. Leave the default options shown and **Click Next**.

    ![Step 4](https://github.com/New-Data-Company/SmartImport_Frontend/blob/master/public/wiki/GitForWindows/Step4.PNG)

    -   [ ] Next, in the **Choosing the default editor used by Git** dialog, unless you're familiar with Vim, we highly recommend using a text editor you're comfortable using. If Sublime Text is available as an option to proceed for you then continue, otherwise continue with Vim and **Click Next**. If you cannot select Sublime we will configure it for use with yoru instance of _Git Bash_ later.

    ![Step 5](https://github.com/New-Data-Company/SmartImport_Frontend/blob/master/public/wiki/GitForWindows/Step5.PNG)

    -   [ ] Next, in the Adjusting your PATH environment, keep the recommended default and use **Git from the command line and also from 3rd-party software** as shown in the image. This option will allow you to use Git from either Git Bash or the Windows Command Prompt.

    ![Step 6](https://github.com/New-Data-Company/SmartImport_Frontend/blob/master/public/wiki/GitForWindows/Step6.PNG)

    -   [ ] Next, in **Choosing HTTPS transport backend**, leave the default Use the OpenSSL library selected.

    ![Step 7](https://github.com/New-Data-Company/SmartImport_Frontend/blob/master/public/wiki/GitForWindows/Step7.PNG)

    -   [ ] In the **Configuring the line ending conversions**, select Checkout Windows-style, commit Unix-style line endings unless you need other line endings for your work.

    ![Step 8](https://github.com/New-Data-Company/SmartImport_Frontend/blob/master/public/wiki/GitForWindows/Step8.PNG)

    -   [ ] In the **Configuring the terminal emulator to use with Git Bash** window, select Use MinTTY (the default terminal of MSYS2).

    ![Step 9](https://github.com/New-Data-Company/SmartImport_Frontend/blob/master/public/wiki/GitForWindows/Step9.PNG)

    -   [ ] On the **Configuring extra options** window, leave the default options checked unless you need symbolic links.

    ![Step 10](https://github.com/New-Data-Company/SmartImport_Frontend/blob/master/public/wiki/GitForWindows/Step10.PNG)

    -   [ ] Now we can choose some of the more experimental options that are still in development. Unless you are very familiar with these options, it is better to leave these uncheked. **Click “Install”** and Git will begin its installation.

    ![Step 11](https://github.com/New-Data-Company/SmartImport_Frontend/blob/master/public/wiki/GitForWindows/Step11.PNG)

    ### Click the Install button

    Once completed, you can check the option to Launch Git Bash if you want to open a Bash command line or, if you selected the Windows command line, run Git from the Windows command line. **Click Finish**.

    ![Step 12](https://github.com/New-Data-Company/SmartImport_Frontend/blob/master/public/wiki/GitForWindows/Step12.PNG)

4. On completion _Pin your Terminal to your Taskbar_ and proceed to configure your project settings.

    ![Step 13](https://github.com/New-Data-Company/SmartImport_Frontend/blob/master/public/wiki/GitForWindows/Step13.PNG)

### First-Time Git Setup

Now that you have Git on your system, you’ll want to do a few things to customize your Git environment. You should have to do these things only once on any given computer; they’ll stick around between upgrades. You can also change them at any time by running through the commands again.

Git comes with a tool called `$ git config` that lets you get and set configuration variables that control all aspects of how Git looks and operates. You can view all of your settings and where they are coming from using:

`$ git config --list --show-origin`

#### Your Identity

The first thing you should do when you install Git is to set your user name and email address. This is important because every Git commit uses this information, and it’s immutably baked into the commits you start creating:

```
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```

Be sure that the information above should match your [GitHub Account](https://www.github.com) login credentials. Again, you need to do this only once if you pass the `--global` option, because then Git will always use that information for anything you do on that system. If you want to override this with a different name or email address for specific projects, you can run the command without the `--global` option when you’re in that project.

#### Configure an Editor (SublimeText3) & add it to your PATH

Now that your identity is set up, you can configure the default text editor that will be used when Git needs you to type in a message. If not configured, Git uses your system’s default editor.

Using [SublimeText](https://sublimetext.com), you will need to [Download and Configure a Windows version](https://sublimetext.com/3) that we will setup to use for this project. Install _SublimeText3_ as per the default installation workflow provided after you complete the download of the Windows executable. Next you need to make sure that the _SublimeText3_ executable is defined in your `PATH` variable so that it can be found when working from the terminal.

In your Windows _System Properties_ dialog box, click on the **Environment Variables** button on the bottom of the prompt and in the **System Variables** tables on the bottom half of the interface look for your **PATH** variable.

-   [ ] _System Properties_ --> _Environment Variables_ --> _System Variables_ --> _PATH_

Click on **EDIT** to add a new variable to your **PATH** that will tell the terminal where to look for SublimeText3. Next, click on **NEW** and add the path to the directory where your `subl.exe` executable file was installed. In my case, I installed Sublime in the default location at:

-   [ ] `C:\Program Files\Sublime Text 3`

Now, from your new _Git Bash_ terminal which should be pinned to your Windows taskbar from here on out, you can enter `$ subl --version` into the command line and you can expect to see the following output:

-   [ ] `Sublime Text Build 3211`

**Complete editor config in Git**

We need to complete the initial configuration of our git profile so you need to do the following:

-   [ ] `$ git config --global core.editor "subl -n -w"`

    -   If the above does not work you can use: `$ git config --global core.editor "'C:/Program\ Files/Sublime\ Text\ 3/sublime_text.exe' -n -w"`

Finally, if you use `$ git config --list` you should see all of the configuration settings that you have just added in your terminal as shown below.

![Step 14](https://github.com/New-Data-Company/SmartImport_Frontend/blob/master/public/wiki/GitForWindows/Step14.PNG)

#### Connecting to GitHub with SSH

For this project you may want to connect to GitHub using SSH to optimize your workflow. Using the SSH protocol, you can connect and authenticate to remote servers and services. With SSH keys, you can connect to GitHub without supplying your username or password at each visit. There are a few key steps that you must accomplish here that you now complete with your new terminal/command line interface installed in previous steps.

-   [ ] Checking for existing SSH keys

Before you generate an SSH key, you can check to see if you have any existing SSH keys:

1. Open Terminal and Enter:

`$ ls -al ~/.ssh` to see if existing SSH keys are present. This will list the files in your .ssh directory, if they exist.

2. Check the directory listing to see if you already have a public SSH key. By default, the filenames of the public keys are one of the following:

-   id_rsa.pub
-   id_ecdsa.pub
-   id_ed25519.pub

If you don't have an existing public and private key pair, or don't wish to use any that are available to connect to GitHub, then generate a new SSH key as we will discuss below.

If you see an existing public and private key pair listed (for example id_rsa.pub and id_rsa) that you would like to use to connect to GitHub, you can add your SSH key to the ssh-agent.

**Tip:** If you receive an error that `~/.ssh` doesn't exist, don't worry! We'll create it when we generate a new SSH key.

3. Generating a new SSH key and adding it to the ssh-agent→

After you've checked for existing SSH keys, you can generate a new SSH key to use for authentication, then add it to the ssh-agent.

-   [ ] Open Terminal

-   [ ] Paste the text below, substituting in your GitHub email address.

    `$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`

    This creates a new ssh key, using the provided email as a label.

    `> Generating public/private rsa key pair.`

-   [ ] When you're prompted to "Enter a file in which to save the key," press Enter. This accepts the default file location.

    `> Enter a file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]`

-   [ ] At the prompt, type a secure passphrase. **PRESS ENTER AND KEEP IT EMPTY & WITHOUT A PASSPHRASE**.

    `> Enter passphrase (empty for no passphrase): [PRESS ENTER]`

    `> Enter same passphrase again: [PRESS ENTER]`

You will get an output response on your terminal letting you know that your identity and key have been saved in the default locations in your home directory. The output in your terminal will include a SHA256 fingerprint that the keygen tool generated for you along with an RSA 4096 randomly generated randomart image.

#### Adding a new SSH key to your GitHub account

To configure your GitHub account to use your new (or existing) SSH key, you'll also need to add it to your GitHub account.

-   [ ] Copy the SSH key to your clipboard.

If your SSH key file has a different name than the example code, modify the filename to match your current setup. When copying your key, don't add any newlines or whitespace.

`$ clip < ~/.ssh/id_rsa.pub`
`# Copies the contents of the id_rsa.pub file to your clipboard`

**Tip:** If clip isn't working, you can locate the hidden .ssh folder in the home directory, open the file in your favorite text editor, and copy it to your clipboard.

In the upper-right corner of any page, click your profile photo, then click Settings.

![Settings icon in the user bar](https://github.com/New-Data-Company/SmartImport_Frontend/blob/master/public/wiki/GitForWindows/Step15.png)

In the user settings sidebar, click SSH and GPG keys.

![Authentication keys](https://github.com/New-Data-Company/SmartImport_Frontend/blob/master/public/wiki/GitForWindows/Step16.png)

Click New SSH key or Add SSH key.

![SSH Key button](https://github.com/New-Data-Company/SmartImport_Frontend/blob/master/public/wiki/GitForWindows/Step17.png)

In the "Title" field, add a descriptive label for the new key. For example, if you're using a personal Mac, you might call this key "Personal MacBook Air".

Paste your key into the "Key" field.

![The key field](https://github.com/New-Data-Company/SmartImport_Frontend/blob/master/public/wiki/GitForWindows/Step18.png)

Click Add SSH key.

![The Add key button](https://github.com/New-Data-Company/SmartImport_Frontend/blob/master/public/wiki/GitForWindows/Step19.png)

If prompted, confirm your GitHub password.

![Sudo mode dialog](https://github.com/New-Data-Company/SmartImport_Frontend/blob/master/public/wiki/GitForWindows/Step20.png)

#### Testing your SSH connection

After you've set up your SSH key and added it to your GitHub account, you can test your connection. When you test your connection, you'll need to authenticate this action using your password, which is the SSH key passphrase you created earlier. For more information on working with SSH key passphrases, see "Working with SSH key passphrases".

Open Terminal.
Enter the following:

`$ ssh -T git@github.com`
`# Attempts to ssh to GitHub`

You may see a warning like this:

```
> The authenticity of host 'github.com (IP ADDRESS)' can't be established.
  > RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
  > Are you sure you want to continue connecting (yes/no)?
```

or like this:

```
> The authenticity of host 'github.com (IP ADDRESS)' can't be established.
  > RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
  > Are you sure you want to continue connecting (yes/no)?
```

Verify that the fingerprint in the message you see matches one of the messages in step 2, then type **yes**:

```
> Hi username! You've successfully authenticated, but GitHub does not
> provide shell access.
```

Verify that the resulting message contains your username.

## Configure your terminal and your bash_profile

Now that your Windows development environment is configured with your Git Version Control and your SublimeText editor as your new project workspace, we need to make sure that our shell prompt is optimized for our workflow by customizing our bash prompt to display information that is important to us throughout each phase of work.

From the terminal, click on the icon in the top left corner of the terminal window to bring up the context menu and select _Options..._.

In the _Options_ dialog, within the _Looks_ section body, find _Colours_, and click on _Background_. In the Color dialog box, select the color _White_ (You can pick any color you like, but this is just what I am using for my personal environment, you can select what you can see with best), and click _OK_ to save your selection and close the dialog box.

Next, click the _Foreground..._ button and select the color _Black_, and click _OK_ to save your selection and close the dialog box. Click **Apply** in the _Options_ dialog box and close and restart your terminal to see the changes.

### Configure your bash_profile

In the sidebar there are three links to files that you need to download and store inside of your computer's home directory. Your home directory is your computer's top level directory where your path finds itself in the terminal after having entered the following command in your terminal: `$ cd`.

Your terminal will display a tilde character or `~` to indicate you are in the home directory. You computer's root directory is indicated with a `/` character in Windows, and this is two directories up which can be accessed by using the `$ cd ..` command twice. Using the `$ cd` command by itself will always take you right back to the home, or `~` directory. Your `home ~` directory is typically going to be the top level directory for the _User_ defined on your Windows machine. On a Windows machine, your home directory is where you will find folders like your `Downloads`, `Documents`, `Desktop`, etc.

-   [ ] Proceed to download the following files and save them in your home directory with the names you see them listed under. In the case of items #2 and #3, you need to create a directory in your home directory called `.terminal-config` where each of those files will be saved under. It is important that your use the period in the file name so that git can access the files saved in the directory programatically.

This will save the file as a hidden file in Windows and can be accessed from the terminal using the `$ ls -a` command. Your `bash_profile` references these files and it is important that you create the folder structure as explained herein so that your terminal can access these bash scripts accordingly.

You will find that you cannot create a new folder as a hidden file from the Windows Explorer interface using the _Create New Folder_ mechanism as you would normally do in Windows. To complete this task you need to use the bash prompt (terminal) and navigate to your home directory to enter the `$ mkdir .terminal-config` command that will create the folder you need to save the filed indicated in items #2 and #3 below.

1. [.bash_profile](https://github.com/New-Data-Company/SmartImport_Backend/wiki/resources/config-tools/nativeStack.bash_profile)

2. [.terminal-config/git-completion.bash](https://github.com/New-Data-Company/SmartImport_Backend/wiki/resources/config-tools/nativeStack-terminal-config/git-completion.bash)

3. [.terminal-config/git-prompt.sh](https://github.com/New-Data-Company/SmartImport_Backend/wiki/resources/config-tools/nativeStack-terminal-config/git-prompt.sh)

Once you have saved all of the files above in the home directory according to the instructions above your terminal should now look something like the image below and you are ready to develop applications using a professional engineering workflow using Git Version Control, SublimeText3, SSH to access your GitHub repositories and everything you need to connect to the AWS cloud.

![Terminal Complete](https://github.com/New-Data-Company/SmartImport_Frontend/blob/master/public/wiki/GitForWindows/Step21.PNG)

The username in purple above is the user account name that you can find in the following windows system path:

-   Control Panel --> User Accounts

The username is the name of directory in `C:\Users` that is created when that user is initially established on the machine. Choose your initial username wisely!
