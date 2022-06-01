# Composer template for Drupal projects
## Package features
### Asset packagist support
The Asset packagist package acts as a bridge between Composer and the popular NPM and Bower repositories, which catalog
thousands of useful front-end and JavaScript packages. This allows developers to easily pull in packages like DropZoneJS
and many others without requiring local Node.js to be installed.

Read more: https://lightning.acquia.com/blog/round-your-front-end-javascript-libraries-composer

### Guardr core security
Guardr is a Drupal distribution with a combination of modules and settings to enhance a Drupal application's security
and availability to meet enterprise security requirements. This project leverages Guardr's package management and
module configuration.

### Sub-profile support
A Drupal core patch has been included to add support for "Sub-profiles".

See: https://www.drupal.org/node/1356276

### Rain base profile features
The [Mediacurrent Rain base install profile](https://bitbucket.org/mediacurrent/mis_rain/) includes many of the most
common packages pre-configured for rapid site development and optional content features.

## Setting up a [DDEV-Local](https://ddev.readthedocs.io/en/stable/) environment

### Clone this repository into the directory of your choice:
- `$ git clone git@github.com:Matt-Hood/scbd.git`

### Install composer on host machine
If you haven't already, install composer:

- On MacOS ```brew install composer```
- Otherwise, see instructions here https://getcomposer.org/

### Build & Start the local environment

- `$ cd scbd.git`
- `$ ddev start`
- `$ ./scripts/build.sh`

This script automates the following steps:

* Runs composer install
* Installs the project Drupal site

The initial pass of the build script downloads several dependencies and an intermittent internet connection will affect the initial build process.

### Troubleshooting
* Ensure ddev has started without errors. Correct errors before proceeding.

## Initial Configuration

### Rename & configure sample 'mis_profile' install profile for continued project development
- Change this to the name of your project name ( Copy contrib/mis_profile directory to custom/profilename)
- Find and replace all instances of 'mis_profile' with your project name
- Enable desired base profile features and modules (see mis_profile.install for more instructions).

## Logging In
* Use `ddev drush uli` to login to your local installation.

## Adding the sync folder to be used with new installs
* The first time build.sh runs successfully you will be able to export configuration back to your project's sync folder.
* Add an empty folder named 'sync' at profile/profilename/config/sync.
* Add `$settings['config_sync_directory'] = $app_root . '/profiles/profilename/config/sync';` to your settings.php.
* Run `ddev drush cex` to export configuration to the sync folder.
* Re-run `$ ./scripts/build.sh` to test install with sync configuration.
* Once this is working as expected, add the sync folder to git and commit.

## Development Settings
* The settings.local.php file contains settings for customizing the development environment.  This disables Drupal's built in caching and additionally activates sites/development.services.yml for further customizing the development environment.

# Development Workflow

* [Use Composer](https://www.drupal.org/docs/develop/using-composer/using-composer-to-manage-drupal-site-dependencies#managing-contributed) to add 3rd party dependencies and patches.
* Write custom modules, themes etc. to the ./web/ directory.
* Run `ddev drush cex` to export Drupal configuration to the profile/profilename/config/sync folder.
* Run `$ ./scripts/build.sh` before starting a new ticket. Run build.sh again to test work completed prior to submitting a pull request.

## Demo Content
* TBD

## Additional Links
* [Project Drupal Theme Guide](https://bitbucket.org/mediacurrent/scbd.git/src/HEAD/web/themes/custom/project_theme/README.md?fileviewer=file-view-default)
* [DDEV-Local Documentation](https://ddev.readthedocs.io/en/stable/)
* This repository created from [Composer template for Drupal projects](https://github.com/drupal-composer/drupal-project/blob/9.x/README.md) which has some addition information on usage.
* [Using Composer](https://www.drupal.org/docs/develop/using-composer) with Drupal.
