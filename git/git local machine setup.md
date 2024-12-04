# Setting git up on your local machine

The basic rundown of using git involves two major steps

1. Install Git
2. Configure Git and GitHub

#### Install git

This will differ given your operating system. [Here](https://www.theodinproject.com/lessons/foundations-setting-up-git#step-1-install-git) is a guide from [The Odin Project](https://www.theodinproject.com/) website.

#### Configure Git and GitHub

Once you've installed, you can begin configuring git for your device and GitHub account.

##### 1. Create a GitHub account on [GitHub](https://github.com/)

##### 2. Setup Git using the following commands

```bash
git config --global user.name "Your Name"
git config --global user.email "yourname@example.com"
#If your email is set to private on GitHub, use the email provided by GitHub, not your actual email address
git config --global init.defaultBranch main
git config --global pull.rebase false
```

##### 3. Verify with the following commands

```bash
git config --get user.name
git config --get user.email
```

##### 4. Set up SSH key

For SSH key, you need to check the following first:

```bash
ls ~/.ssh/id_ed25519.pub
```

If the file does not exist, do the following:

```bash
ssh-keygen -t ed25519
```

##### 5. Link SSH key with GitHub

On GitHub, got to `Settings` then click `SSH and GPG keys`. Click the green `New SSH Key` button. Name the key something descriptive and memorable - I recommend your device name. Then, in your terminal, run the following command:

```bash
cat ~/.ssh/id_ed25519.pub
```

Then, copy the entire output of the `cat` command and on Github, paste the copied text into the key field. Keep the key type as `Authentication Key` and click `Add SSH key`.

##### 6. Test your key

```bash
ssh -T git@github.com
```

If everything worked as it should, you should receive the following output:

```
> The authenticity of host 'github.com (IP ADDRESS)' can't be established.
> ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
> Are you sure you want to continue connecting (yes/no)?
```

Click yes and you should see

```
> Hi USERNAME! You've successfully authenticated, but GitHub does not
> provide shell access.
```

If not, rerun the steps above. If you selected private email, then you have to check on GitHub what the publically accessible email is. You can check this under `Email Settings` on GitHub.