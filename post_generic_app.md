# Post-Generic App To Do List

This document covers the tasks you should do after using the Generic App gem to start a new Ruby on Rails project.  For a less serious project, you may be able to skip some of the tasks to save time.  For a very serious project, do not skip any of the tasks below.

## Getting Started
* Start tmux.  Go to your new app's root directory.
* Enter your new app's root directory.
* Enter the command "sh credentials.sh".  (NOTE: If you are not using Heroku, remove the Heroku section in this script.)
* Enter the command "sh build_fast.sh; sh server.sh".  Open your web browser to the appropriate URL to view your app locally.  (NOTE: The build_fast.sh script takes a few minutes to test your app, outline your app, and seed the database.)  
* Start a second tmux window, and go to your new app's root directory.  Enter the following commands:
```
git add .
git commit -m "Initial commit"
```
* Start a Git repository for your new app, and push your new app into that repository.
* Deploy this app.  Instructions for deploying to Heroku are at https://github.com/rubyonracetracks/cheat_sheets/blob/master/rails_heroku.md.
* Add continuous integration badges to your README.md page.  Instructions are at https://github.com/rubyonracetracks/cheat_sheets/blob/master/continuous_integration.md.
* Enable the email capability in the production environment.  (Unlike the development and testing environments, the production environment requires custom settings.)  More details are at https://gist.github.com/jhsu802701/7fe586085ee05b172349ab896fed50be .
* Convert the development environment from this app from SQLite to PostgreSQL.  More instructions are provided below.
* Set the Ruby version of your app.  More instructions are provided below.
* Update the README.md file in your app.  More instructions are provided below.
* Reset your development environment.  More instructions are at https://gist.github.com/jhsu802701/f9a536446648f5335f1d4723fd65665a .
* Don't forget to maintain your new app over time.  More instructions are provided below.

## Switching from SQLite to PostgreSQL
* Enter the command "sh pg_setup.sh".  When prompted, enter your desired username and password.  Remember that your username and password are NOT saved in the source code.
* Enter the command "sh git_check.sh".  All tests should pass, and there should be no offenses.
* Enter the following commands:
```
git add .
git commit -m "Converted from SQLite to PostgreSQL"
git push origin master
```
* Enter the command "sh heroku.sh".

## Set the Ruby Version of Your App
* Enter the command "ruby -v" to get the current version of Ruby in use.
* Add the following line to the beginning of your Gemfile:
```
ruby 'x.y.z'
```
* Replace "x.y.z" with the current version of Ruby in use.
* Enter the command "sh git_check.sh".  All tests should pass, and there should be no offenses.
* Enter the following commands:
```
git add .
git commit -m "Set the Ruby version in the Gemfile"
git push origin master
```
* Enter the command "sh heroku.sh".

## Updating the README.md File
* Add in additional information for developers, such as the URL where the app is deployed.
* Enter the following commands:
```
git add .
git commit -m "Updated the README.md file"
git push origin master
```


## Maintenance
* Create a custom Docker image for this project.  The initial Docker image should include the version of Ruby you are currently using in this app.  When a new version of Ruby becomes available, update your Docker image to include this new version.
* For each version of Ruby preinstalled in your Docker image, you should also include the mailcatcher gem and the current and expected future versions of the rails gem, the pg gem, the nokogiri gem, and any other gems that take a long time to install.  This makes it easier to upgrade the Gemfile.  (And if the upgrades require more work than anticipated, you can stick to the old versions until you resolve the upgrade issues.)
* Run the upgrade_gems.sh script.
* Upgrade the gem versions (other than rails/pg/nokogiri) in the Gemfile.
* Upgrade the Ruby version of this app and the Ruby versions preinstalled in the custom Docker image.
* Upgrade the rails/pg/nokogiri/ffi versions in the Gemfile and in the custom Docker image.
