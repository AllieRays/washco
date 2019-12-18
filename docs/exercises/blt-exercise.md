# Blt exercise for Windows

## Create your project locally

Git clone the project
`git clone git@github.com:AllieRays/washco.git`

## Setup dependencies

In order to use BLT and Drupal VM, your machine should have several
dependencies available. Before continuing, ensure you have the following
installed:

1. Install xcode (required for git)
```
sudo xcodebuild -license
xcode-select --install
```

2. Install the minimum dependencies for Acquia BLT.
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew install php73 git composer
composer global require "hirak/prestissimo:^0.3"
 ```

3. Install drush launcher
See the Drush Launcher installation instructions here:
https://github.com/drush-ops/drush-launcher#installation---phar
Must be using Drush 9 and above. 
Verify drush launcher was installed correctly:
```
// Should report "Drush Launcher Version: #.#.#"
drush --version
```
Note: if you don't see the drush launcher version reported, you may have another
drush executable in your path. Devdesktop for example adds lines to
~/.bash_profile and/or ~/.bashrc that may need to be removed or adjusted.

4. Install vagrant, virtualbox, and ansible for Drupal VM.
```
brew tap caskroom/cask
brew install ansible
brew cask install virtualbox vagrant
```


# Check out blt-pipelines-integration branch

`git checkout blt-pipelines-integration branch `


# Setup Local Environment.

BLT provides an automation layer for testing, building, and launching Drupal 8 applications. For ease when updating codebase it is recommended to use  Drupal VM. If you prefer, you can use another tool such as Docker, [DDEV](https://docs.acquia.com/blt/install/alt-env/ddev/), [Docksal](https://docs.acquia.com/blt/install/alt-env/docksal/), [Lando](https://docs.acquia.com/blt/install/alt-env/lando/), (other) Vagrant, or your own custom LAMP stack, however support is very limited for these solutions.
1. Install Composer dependencies.
After you have cloned the project and setup your blt.yml file install Composer Dependencies. (Warning: this can take some time based on internet speeds.)
    ```
    $ composer install
    ```

2. Setup a local blt alias.
If the blt alias is not available use this command outside and inside vagrant (one time only).
    ```
    $ composer run-script blt-alias
    ```

3. Setup VM.
Start the VM  
    ```
    // This command should be run once.
    $ blt vm
    
    // Once `blt vm` has been run, the following should be used to boot the vm.
    $ vagrant up
    ```

4. SSH into your VM.
SSH into your localized Drupal VM environment automated with the BLT launch and automation tools.
    ```
    $ vagrant ssh
    ```
   
5. Setup your local settings.php file for development.
Go to docroot/sites/default/settings/local.settings.php and fill in the following key value attributes. You can find these values on the dev server here

for example 
```
$config['key.key.keygen']['key_provider_settings']['key_value'] = '';
```

6. Setup your local site from a remote db. This command will use the configured
drush remote alias in blt/blt.yml (or blt/local.blt.yml):
   ```
   $ blt setup
   ```
   

7. Setup your local site from a remote db. This command will use the configured
drush remote alias in blt/blt.yml (or blt/local.blt.yml):
   ```
   $ blt sync:refresh
   ```


8. Run blt doctor
   ```
   $ blt docotor
   ```
