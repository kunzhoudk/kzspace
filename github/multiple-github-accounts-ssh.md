# Using Multiple GitHub Accounts and SSH Keys

Creating an SSH key is an excellent authentication method when working with GitHub. However, sometimes you need to work with multiple GitHub accounts on the same system, like a work account and a personal account. To accomplish this, you can create multiple SSH keys and associate each one with different GitHub accounts. In this tutorial, you will learn how to configure and manage these multiple accounts and SSH keys for authenticating with multiple GitHub accounts.

## 1 - Generate SSH keys

Before generating an SSH key, we can check if we have any existing SSH keys: `ls -al ~/.ssh` , which will list out all existing public and private key pairs, if any.

If `~/.ssh/id_rsa` is available, we can reuse it, or else we can first generate a key to the default `~/.ssh/id_rsa` by running:
  * `ssh-keygen -t rsa`
  
When asked for the location to save the keys, accept the default location by **pressing enter**. A private key and public key `~/.ssh/id_rsa.pub` will be created at the default ssh location `~/.ssh/`. Let’s use this default key pair for our personal account.

### 1.1 Generate SSH key for work account 

For the work accounts, we will create different SSH keys using:
* `$ ssh-keygen -t rsa -C "email@work_mail.com" -f "id_rsa_work"`
  which will generate the SSH keys, and saves the public key with the tag “*email@work_mail.com*” to `~/.ssh/id_rsa_work_.pub`

## 2 - Adding the new SSH key to the corresponding GitHub account
We already have the SSH public keys ready, and we will ask our GitHub accounts to trust the keys we have created. This is to get rid of the need for typing in the username and password every time you make a Git push.

Copy the public key `pbcopy < ~/.ssh/id_rsa.pub` and then log in to your personal GitHub account:

  - Go to **Settings**
  - Select **SSH and GPG keys** from the menu to the left.
  - Click on **New SSH key**, provide a suitable title, and paste the key in the box below.
  - Click **Add key** and you’re done!

## 3 - Registering the new SSH Keys with the ssh-agent
To use the keys, we have to register them with the ssh-agent on our machine. Ensure ssh-agent is running using the command `eval "$(ssh-agent -s)"`. Add the keys to the ssh-agent like so:
   *  `ssh-add ~/.ssh/id_rsa`
   *  `ssh-add ~/.ssh/id_rsa_work`

## 4 - Creating the SSH config File

Here we are actually adding the SSH configuration rules for different hosts, stating which identity file to use for which domain.

The SSH config file will be available at `~/.ssh/config`. Edit it if it exists, or else we can just create it.

```
$ cd ~/.ssh/
$ touch config           // Creates the file if not exists
$ code config            // Opens the file in VS code, use any editor
```

Make configuration entries for the relevant GitHub accounts similar to the one below in your `~/.ssh/config` file:

```
# Personal account, - the default config
Host github.com        // can be also in any name, like "kunzhou"
   HostName github.com
   User git
   IdentityFile ~/.ssh/id_rsa
   
# Work account-1
Host github.com-work    // can be also in any name, like "agco" 
   HostName github.com
   User git
   IdentityFile ~/.ssh/id_rsa_work_user1
```

**“work”** is the GitHub user id for the work account. **“github.com-work”** is a notation used to differentiate the multiple Git accounts. You can also use any name, such as you company name “agco” notation as well. Make sure you’re consistent with what hostname notation you use. This is relevant when you clone a repository or when you set the remote origin for a local repository.

The above configuration asks ssh-agent to:

  * Use **id_rsa** as the key for any Git URL that uses **@github.com**
  * Use the **id_rsa_work** key for any Git URL that uses **@github.com-work**

## 5 - While Cloning Repositories
Note: step 6 will help, if we have the repository already available on local.

Now that the configurations are in place, we can go ahead and clone the corresponding repositories. On cloning, make a note that we use the host names that we used in the SSH config.

Repositories can be cloned using the clone command Git provides:

```git 
git clone git@github.com:personal_account_name/repo_name.git
```
The work repository will require a change to be made with this command:
```git 
git clone git@github.com-work:OperationsManagement/ora.git
```
This change is made depending on the host name defined in the SSH config. The string between **@ and :** should replaced by **Host** we have given in the SSH config file.

## 6 - For Locally Existing Repositories

If we have the repository already cloned, and list the Git remote of the repository using `git remote -v`.

Check whether the URL matches our GitHub host to be used, otherwise update the remote origin URL.

```git
git remote set-url origin git@github.com-worker:OperationsManagement/ora.git
```

**Sources**
* https://www.freecodecamp.org/news/manage-multiple-github-accounts-the-ssh-way-2dadc30ccaca/
* https://jeffbrown.tech/multiple-github-accounts-ssh/
