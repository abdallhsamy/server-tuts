# How To Install and Use Composer on Ubuntu 20.04
## Introduction
[Composer]( https://getcomposer.org/) is a popular dependency management tool for PHP, created mainly to facilitate installation and updates for project dependencies. It will check which other packages a specific project depends on and install them for you, using the appropriate versions according to the project requirements. Composer is also commonly used to bootstrap new projects based on popular PHP frameworks, such as [Symfony]( https://symfony.com) and [Laravel]( https://laravel.com).
In this tutorial, you’ll install and get started with Composer on an Ubuntu 20.04 system.
## Prerequisites
In order to follow this guide, you will need access to an Ubuntu 20.04 server as a non-root sudo user, and a firewall enabled on your server. To set this up, you can follow our [initial server setup guide for Ubuntu 20.04]( https://github.com/abdallhsamy/server-tuts/blob/master/initial-server-setup-with-ubuntu-20.04..md).
## Step 1 — Installing PHP and Additional Dependencies
In addition to dependencies that should be already included within your Ubuntu 20.04 system, such as `git` and `curl`, Composer requires `php-cli` in order to execute PHP scripts in the command line, and `unzip` to extract zipped archives. We’ll install these dependencies now.
First, update the package manager cache by running:
```
sudo apt update
```
Next, run the following command to install the required packages:
```
sudo apt install php-cli unzip
```
You will be prompted to confirm installation by typing `Y` and then `ENTER`.
Once the prerequisites are installed, you can proceed to installing Composer.
## Step 2 — Downloading and Installing Composer
Composer provides an [installer]( https://getcomposer.org/installer) script written in PHP. We’ll download it, verify that it’s not corrupted, and then use it to install Composer.
Make sure you’re in your home directory, then retrieve the installer using `curl`:
```
cd ~
curl -sS https://getcomposer.org/installer -o composer-setup.php
```
Next, we’ll verify that the downloaded installer matches the SHA-384 hash for the latest installer found on the [Composer Public Keys / Signatures page]( https://composer.github.io/pubkeys.html). To facilitate the verification step, you can use the following command to programmatically obtain the latest hash from the Composer page and store it in a shell variable:
```
HASH=`curl -sS https://composer.github.io/installer.sig`
```
If you want to verify the obtained value, you can run:
```
echo $HASH
```
**Output**
```
e0012edf3e80b6978849f5eff0d4b4e4c79ff1609dd1e613307e16318854d24ae64f26d17af3ef0bf7cfb710ca74755a
```
Now execute the following PHP code, as provided in the Composer [download page]( https://getcomposer.org/download/), to verify that the installation script is safe to run:
```
php -r "if (hash_file('SHA384', 'composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
```
You’ll see the following output:
**Output**
```
Installer verified
```
If the output says `Installer corrupt`, you’ll need to download the installation script again and double check that you’re using the correct hash. Then, repeat the verification process. When you have a verified installer, you can continue.
To install `composer` globally, use the following command which will download and install Composer as a system-wide command named `composer`, under `/usr/local/bin`:
```
sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
```
You’ll see output similar to this:
**Output**
```
All settings correct for using Composer
Downloading...

Composer (version 1.10.5) successfully installed to: /usr/local/bin/composer
Use it: php /usr/local/bin/composer
```
To test your installation, run:
```
composer
```
**Output**
```
   ______
  / ____/___  ____ ___  ____  ____  ________  _____
 / /   / __ \/ __ `__ \/ __ \/ __ \/ ___/ _ \/ ___/
/ /___/ /_/ / / / / / / /_/ / /_/ (__  )  __/ /
\____/\____/_/ /_/ /_/ .___/\____/____/\___/_/
                    /_/
Composer version 1.10.5 2020-04-10 11:44:22

Usage:
  command [options] [arguments]

Options:
  -h, --help                     Display this help message
  -q, --quiet                    Do not output any message
  -V, --version                  Display this application version
      --ansi                     Force ANSI output
      --no-ansi                  Disable ANSI output
  -n, --no-interaction           Do not ask any interactive question
      --profile                  Display timing and memory usage information
      --no-plugins               Whether to disable plugins.
  -d, --working-dir=WORKING-DIR  If specified, use the given directory as working directory.
      --no-cache                 Prevent use of the cache
  -v|vv|vvv, --verbose           Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
...
```
This verifies that Composer was successfully installed on your system and is available system-wide.
> **Note**: If you prefer to have separate Composer executables for each project you host on this server, you can install it locally, on a per-project basis. This method is also useful when your system user doesn’t have permission to install software system-wide.
> To do this, use the command `php composer-setup.php`. This will generate a `composer.phar` file in your current directory, which can be executed with `php composer.phar`.
## Conclusion
Composer is a powerful tool that can greatly facilitate the work of managing dependencies in PHP projects. It provides a reliable way of discovering, installing, and updating PHP packages that a project depends on. In this guide, we saw how to install Composer, how to include new dependencies in a project, and how to update these dependencies once new versions are available.

