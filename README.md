# Terraform Beginner Bootcamp 2023

## Semantic Versioning! :mage:

THis project is going to utilize semantic versioning for its tagging.
[semver.org](https://semver.org/)

The general format:

**MAJOR.MINOR.PATCH**, eg. `1.0.1`

- **MAJOR** version when you make incompatible API changes
- **MINOR** version when you add functionality in a backward compatible manner
- **PATCH** version when you make backward compatible bug fixes
Additional labels for pre-release and build metadata are available as extensions to the MAJOR.MINOR.PATCH format.

## Install the Terraform CLI

### Considerations with the Terraform CLI changes
The Terraform CLI installation instructions have changed due to gpg keying changes. So the original gitpod.yml bash

[Install Terraform CLI](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)


### Refactoring into Bash scripts
While fixing the Terraform CLI gpg depreciation issues we notice that bash scripts steps were a considerable amount more code. So we decided to create a bash script to install the Terraform CLI. 

This bash script is located here: [./bin/install_terraform_cli.sh](./bin/install_terraform_cli.sh)

### Consideration of Linux distribution

This project is built against Ubuntu.
Please consider checking your Linux Distribution and change accordingly to distribution needs.

(How to Check OS version in Linux)[https://www.cyberciti.biz/faq/how-to-check-os-version-in-linux-command-line/]

```cat /etc/os-release```

### Shebang Considerations

A Shebang (Pronounced Sha-bang) tells the bash script what program that will interpret the script.

ChatGPT recomended this format for bash ```#!/bin/bash```

- for portability for different OS distribution
(Intro to Shebang)[https://en.wikipedia.org/wiki/Shebang_(Unix)]

### Execution Consideration

When executing he bash script we can use the `./` shorthand notiation to associate the bash script. 

eg. `./bin/install_terraform_cli`

If we are using a script in .gitpod.yml we need to point the script to a program to interpret it.

eg. ```source ./bin/install_terraform_cli```

To make the file executable use chmod

eg. ```chmod u+x ./bin/install_terraform_cli```

### gitpod lifecycle (Before, Init, Command)

We need to be careful when using the Init because it will not rerun if we restart an existsing workspace
(Intro to Gitpod Tasks)[https://www.gitpod.io/docs/configure/workspaces/tasks]

### Working Env vars

#### env command

We can list out all Environmant Variables (Env vras) using the `env` command

We can filter specific env vars using grep eg. `env | grep AWS_`

#### setting and unsetting Env vars

In the terminal we can set using `export HELLO='world'`

In the terminal we unset using `unset HELLO`

we can set an env var temporarily when just running a command

```sh
HELLO='world' ./bin/print_message
```
Within a bash script we can set env without writing export eg.

```
sh
#!/usr/bin/env bash

HELLO='world'

echo $HELLO
```

#### Printing Vars

We can print an env var using echo eg. `echo $HELLO`

#### Scoping of Env vars

When you open up new bash terminals in VSCODe it will not be aware of env vars that you have set in another window.

If you want to ENV vars to persist across all future bash terminals that are open you need to set env vars in your bash profile eg. `.bash_profile`

#### Persisting Env vars in Gitpod

We can persist env vars in to gitpod by storing them in gitpod secrest storage

```
gp env HELLO='world'
```

All future workspaces launched wil set the env vars for all bash terminals opened in those workspaces.

You can also set an en vars in teh `.gitpod.yml` but this can only contain non-sensitive env vars.

