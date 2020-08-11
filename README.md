
# Pre-Requisites

Before setting up Drupal 8 on App Engine Flexible, you will need to complete the following:
1. Install Git , php and Composer
2. Create a [Google Cloud Platform project](https://console.cloud.google.com/). Note your Project ID, as you will need it later.
3. Create a [Google Cloud SQL instance](https://cloud.google.com/sql/docs/getting-started) with Public IP. Note down the Instance details You will use this as your Drupal MySQL backend.
4. Install [Gcloud SDK](https://cloud.google.com/sdk/install)

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

 >Configrue Site --> Confiure the site with preffered username and password

 3. Press Ctrl+ C or Cmd + C to kill the local server

4. Execute below command

```sh
composer require "ext-gd:*" --ignore-platform-reqs
```
4. 

***Add app.yaml***

Add a file app.yaml with the following contents to the root of your Drupal project:

```sh
runtime: php
env: flex
service: drupal

runtime_config:
  document_root: .
```

***Deploy Drupal to App Engine***

```sh
gcloud app deploy
```
1. Wait for 5-10 mins 

2. Go to [GCP App Engine Page](https://console.cloud.google.com/appengine) --> Versions

3. Click on the version and you should be able to see the druapl site on GCP App Engine
