## Create and add a ssh key
Follow [this](https://docs.gitlab.com/ee/user/project/repository/gpg_signed_commits/index.html) tutorial.
If you are using Ubuntu 16.04, use the `gpg2` command.

## Project specific verify settings
You can set the git signing settings on a per-project base.
Use the following commands to sign the commits in a project with your gpg key.
```bash
git config user.signingkey YOURKEY
git config commit.gpgsign true
```

## Ubuntu 16.04
If you use Ubuntu 16.04, you have to use `gpg2` instead of `gpg`.
To make GIT use GPG2 as well, use the following command:
```bash
git config --global gpg.program gpg2
```

## Use with IDE (PHPStorm etc.)
To use git signing with your IDE, you will have to edit your GnuPG configuration.
```bash
nano ~/.gnupg/gpg.conf
```
Add these lines to the end of your configuration:
```bash
no-tty
use-agent
```