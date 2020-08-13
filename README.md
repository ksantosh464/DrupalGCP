
# Prerequisites

Before setting up Drupal 8 on App Engine Flexible, you will need to complete the following:
1. Install Git , PHP and Composer
2. Create a [Google Cloud Platform project](https://console.cloud.google.com/). Note your Project ID, as you will need it later.
3. Create a [Google Cloud SQL instance](https://cloud.google.com/sql/docs/getting-started) with Public IP. Note down the Instance details You will use this as your Drupal MySQL backend.
4. Install [Gcloud SDK](https://cloud.google.com/sdk/install)
5. git clone the repo using below command in your local machine
```sh
git clone https://github.com/ksantosh464/DrupalGCP
```

# Install Drupal 8.9

 Use the Drupal 8 Drush CLI to install a drupal project. This can be installed locally by running composer install in this directory:

```sh
cd DrupalGCP
composer install
./vendor/bin/drush
```

Now you can run the command to download drupal:

```sh
./vendor/bin/drush dl drupal
```
# Installation

  1. Set up your Drupal 8 instance using the web interface

  ```sh
  cd drupal-8.9.3
  php -S localhost:8080
  ```
  2. Open [http://localhost:8080](http://localhost:8080) in your browser after running these steps

> Choose Language --> English

> Choose PROFILE -->  Standard

 >Verify Requirements

 > Setup Database --> Provide the details of  MySQL Cloud SQL ( Instance Name, username, password, IP address and Port)

 >Install Site --> Install

 >Configrue Site --> ConfiGure the site with preferred username and password

 3. Press Ctrl+ C or Cmd + C to kill the local server

4. Execute below command

```sh
composer require "ext-gd:*" --ignore-platform-reqs
```
5. Execute below command

````
cp sites/example.settings.local.php sites/default/settings.local.php
````

6. Execute below command

````
./vendor/bin/drush pm-enable config -y
./vendor/bin/drush config-set system.performance css.preprocess 0
./vendor/bin/drush config-set system.performance js.preprocess 0
````
***Add app.yaml***


Create a file with name ***app.yaml*** with the following contents to the root of your Drupal project:

```sh
runtime: php
env: flex
service: drupal

runtime_config:
  document_root: .
```

***Deploy Drupal to App Engine***

```sh
gcloud app deploy --version v1
```
1. Wait for 5-10 mins 

2. Go to [GCP App Engine Page](https://console.cloud.google.com/appengine) --> Versions

3. Click on the version v1 and you should be able to see the Drupal site on GCP App Engine
