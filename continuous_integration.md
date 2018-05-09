# Continuous Integration
Continous integration is a safeguard against the infamous "works on my machine" problem.  It can also be used to make it much easier to check for outdated gems and potential security problems.  The resulting continuous integration badges should be posted on the README.md file of your app.

## Travis CI (For Rails Apps)
* I prefer Travis CI for testing Rails apps because it's simple to configure.
* I don't like Travis CI for testing Ruby gems, because configuring it to test the gem in a new version of Ruby requires changing the source code.
* URL: https://travis-ci.org/
* Log in to the Travis CI web site and select your new Rails app as one to be monitored.
* Enter the following commands in your local terminal within your app's root directory:
```
touch .travis.yml
touch config/database.yml.travis
```
* Give the config/database.yml.travis file the following content:
```
test:
  adapter: postgresql
  database: travis_ci_test
```
* Give the .travis.yml file the following content:
```
language: ruby
rvm:
 - x.y.z

services:
  - postgresql

before_script:
  - psql -c 'create database travis_ci_test;' -U postgres
  - cp config/database.yml.travis config/database.yml

cache:
  bundler: true
  directories:
    - vendor/cache
```
* In your local terminal, enter the command "ruby -v" to see which version of Ruby you are using.
* In the .travis.yml file, replace "x.y.z" with the version number of Ruby in use.  (Omit the "p" and everything that comes after it.)
* Enter the following commands:
```
git add .
git commit -m "Configured for Travis CI"
git push origin master
```
* Go back to the Travis CI site.  Travis CI will test your app.  This will take a few minutes.  Subsequent Travis builds will be faster, because you have configured Travis to cache the gems installed with the "bundle install" command.
* If all goes well, all tests will pass.
* Add the Markdown code for the Travis status badge to the README.md file just after the top heading.
* To commit the Travis CI badge to the source code, enter the following commands:
```
git add .
git commit -m "Added the Travis CI badge"
git push origin master
```
* The Travis CI badge should now appear on the README.md page of the source code.

## Semaphore CI (For Ruby Gems)
* I prefer Semaphore CI for testing Ruby gems, because it's simple to configure and does not require changing the source code, not even if you need to test your gem in a newer version of Ruby.
* I do not use Semaphore CI for testing Rails apps because it conflicts with my preferred way of setting up PostgreSQL.
* URL: https://semaphoreci.com/
* Add the Markdown code for the Semaphore status badge to the README.md file just after the top heading.
* To commit the Semaphore CI badge to the source code, enter the following commands:
```
git add .
git commit -m "Added the Semaphore CI badge"
git push origin master
```
* The Semaphore CI badge should now appear on the README.md page of the source code.

## CircleCI (Not Recommended)
* NOTE: I am phasing out my use of CircleCI because version 2 requires having a complex configuration file in the source code.
* CircleCI runs all tests to make sure that they pass.
* URL: https://circleci.com/
* NOTE: Adding the configuration file is optional.
* The first build will fail if your project is a Ruby gem.  To resolve the error message saying that you have the wrong (older) version of bundler, go to your project's Dependency Commands settings.  In the pre-dependency commands, add "gem install bundler".  When you rebuild your project, all tests should pass.

## Gemnasium
* Gemnasium checks for outdated gems and insecure gems.
* URL: https://gemnasium.com/
* Log in to the Gemnasium web site and select your new app as one to be monitored.
* Add the Markdown code for the Gemnasium badge to the README.md file.
* Enter the following commands:
```
git add .
git commit -m "Added the Gemnasium badge"
git push origin master
```
* The Gemnasium badge should now appear on the README.md page of the source code.

## Hakiri
* Hakiri checks for security issues.
* URL: https://hakiri.io/
* Log in to the Hakiri web site and select your new app as one to be monitored.
* Add the Markdown code for the Hakiri badge to the README.md file.
* If Hakiri does not recognize one of your GitHub organizations, go to "Account Settings", and change your permissions to "private access".  Select the option to add your GitHub organization.  Once you see that Hakiri has access to the organization, you can change your Hakiri permissions back to "open source dev access".
* If you created your project with Rails Neutrino or GenericApp, there will be five issues flagged as possible security flaws.
* You should mark the following four issues as false positives.
  * app/views/admins/index.html.erb is flagged for a dynamic render path.
  * app/views/users/index.html.erb is flagged for a dynamic render path.
  * app/views/admins/show.html.erb is flagged for cross-site scripting.
  * app/views/users/show.html.erb is flagged for cross-site scripting.
* Add the Markdown code for the Hakiri badge to the README.md file.
* Enter the following commands:
```
git add .
git commit -m "Added the Hakiri badge"
git push origin master
```
* The Gemnasium badge should now appear on the README.md page of the source code.  There is still one critical security warning that has not been addressed yet.
* The one remaining issue is that the Cross-Site Request Forgery in app/controllers/application_controller.rb.  To correct it, edit the file app/controllers/application_controller.rb and add the following line just after the line "class ApplicationController < ActionController::Base":
```
  protect_from_forgery with: :exception
```
* Enter the command "sh git_check.sh".  All tests should pass, and there should be no offenses.
* Enter the following commands:
```
git add .
git commit -m "Resolved the Cross-Site Request Forgery"
git push origin master
```
* Now all security issues raised by Hakiri should be resolved.

## CodeClimate (GPA and Test Coverage)
Go to https://github.com/rubyonracetracks/cheat_sheets/blob/master/codeclimate.md for more details.

## Updating the README.md File
* When the badges for your new project are ready, add the Markdown code for each integration badge to the README.md file.
* Enter the following commands:
```
git add .
git commit -m "Added continuous integration badges"
git push origin master
```
