# Multiple-Github-Accounts
How to Use Multiple GitHub Accounts on the Same Machine

<br ><br >
## Introduction
Working with multiple GitHub accounts on the same machine can be challenging, especially when it comes to managing separate SSH keys and repositories. In this article, we will guide you through the process of setting up and using multiple GitHub accounts on your computer, making your development workflow more efficient and organized.
<br ><br >


## Understanding SSH Keys
SSH (Secure Shell) keys are a secure method for authenticating your computer with remote servers like GitHub. When you connect to a remote server, the server checks the public key you provide against its own list of authorized keys. If the key you provide matches one on the server, you'll be granted access.

Using different SSH keys for each GitHub account helps you keep your work and personal repositories separate and secure.
<br ><br >


## Generating SSH Keys
### Generate a new SSH key
To generate a new SSH key for each GitHub account, open your terminal and run the following command, replacing "your_email@example.com" with the email address associated with the GitHub account:
```
ssh-keygen -t ed25519 -C "your_email@example.com"
```
When prompted for a file in which to save the key, choose a unique name and location, such as `~/.ssh/id_ed25519_account1.`
<br ><br >

### Add the SSH key to the SSH agent
To add the newly generated SSH key to the SSH agent, run these commands in your terminal:
```
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519_account1
```
Repeat these steps for each GitHub account you want to add, remembering to replace the file paths with the unique names you chose earlier.
<br ><br >


## Configuring GitHub Accounts
### Configure your first GitHub account
To configure your first GitHub account, create a new file called config in the ~/.ssh directory. In this file, add the following lines, replacing "Account1" with a descriptive name for your first account:
```
Host github.com-Account1
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_account1
```
<br ><br >

### Configure your second GitHub account
To configure your second GitHub account, add the following lines to the same config file, replacing "Account2" with a descriptive name for your second account and updating the file path to match the second SSH key:
```
Host github.com-Account2
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_account2
```
<br ><br >

### Test the configuration
To test your configuration, run the following command for each account, replacing "github.com-Account1" with the correct Host value from your config file:
```
ssh -T git@github.com-Account1
```
If your configuration is correct, you should see a message from GitHub welcoming you as the user associated with the corresponding SSH key.
<br ><br >


## Managing Multiple Repositories
### Cloning a repository
To clone a repository from one of your GitHub accounts, use the following command, replacing “github.com-Account1” with the appropriate Host value and “your_username” and “your_repository” with the correct information:
```
git clone git@github.com-Account1:your_username/your_repository.git
```
<br ><br >

### Pushing changes to a repository
To push changes to a repository, navigate to the local repository folder and execute the following commands:
```
git add .
git commit -m "Your commit message"
git push
```
Ensure that the local repository is correctly set up to push to the correct remote repository associated with the correct account.
<br ><br >

### Switching between accounts
To switch between accounts when working with different repositories, simply use the appropriate Host value from your `config` file when cloning, fetching, or pushing changes.
<br ><br >


## Troubleshooting Common Issues
If you encounter issues when working with multiple GitHub accounts, double-check your `config` file for typos or errors. Ensure that your SSH keys are correctly generated and added to the SSH agent. Finally, verify that the correct Host value is being used when working with repositories.
<br ><br >


## Best Practices for Managing Multiple GitHub Accounts
To make the most of your multiple GitHub accounts and streamline your workflow, follow these best practices:
<br >
### Organize your repositories
Create a folder structure on your local machine that separates your repositories by account. This will help you keep track of which repositories belong to which account and minimize confusion.
<br ><br >

### Consistent naming conventions
Use consistent naming conventions for your SSH keys, Host values in the config file, and local repository folders. This will make it easier for you to remember which key and Host value correspond to which account.
<br ><br >

### Leverage Git aliases
Git aliases can simplify your workflow when working with multiple GitHub accounts. For example, you can create aliases for frequently used commands with specific account information, like cloning a repository. To create an alias, run the following command:
```
git config --global alias.clone-account1 'clone git@github.com-Account1'
```
Now, when you want to clone a repository from your first account, you can use the alias:
```
git clone-account1:your_username/your_repository.git
```
<br ><br ><br ><br >


Reference : https://www.ayyaztech.com/blog/how-to-use-multiple-github-accounts-on-the-same-machine
