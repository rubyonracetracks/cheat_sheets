# Continuous Integration
Continous integration is a safeguard against the infamous "works on my machine" problem.  It can also be used to make it much easier to check for outdated gems and potential security problems.  The resulting continuous integration badges should be posted on the README.md file of your app.

## Travis CI
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

## Semaphore CI
* I prefer Semaphore CI for testing Ruby gems, because it's simple to configure and does not require changing the source code, not even if you need to test your gem in a newer version of Ruby.
* I do not use Semaphore CI for testing Rails apps because it conflicts with my preferred way of setting up PostgreSQL.
* URL: https://semaphoreci.com/

## CircleCI
* NOTE: I am phasing out my use of CircleCI because version 2 requires having a complex configuration file in the source code.
* CircleCI runs all tests to make sure that they pass.
* URL: https://circleci.com/
* NOTE: Adding the configuration file is optional.
* The first build will fail if your project is a Ruby gem.  To resolve the error message saying that you have the wrong (older) version of bundler, go to your project's Dependency Commands settings.  In the pre-dependency commands, add "gem install bundler".  When you rebuild your project, all tests should pass.

## Gemnasium
* Gemnasium checks for outdated gems and insecure gems.
* URL: https://gemnasium.com/

## Hakiri
* Hakiri checks for security issues.
* URL: https://hakiri.io/
* If you created your project with Rails Neutrino or GenericApp, there will be three issues flagged as possible security flaws.  You should mark these as false positives.
  * app/views/admins/index.html.erb is flagged for a dynamic render path.
  * app/views/users/index.html.erb is flagged for a dynamic render path.
  * app/views/admins/show.html.erb is flagged for cross-site scripting.
  * app/views/users/show.html.erb is flagged for cross-site scripting.
* As of 1-26-2018, there are 4 SQL injection warnings.  This will be resolved in Rails 5.2.

## CodeClimate (GPA and Test Coverage)
Go to https://gist.github.com/jhsu802701/fd33d8947aa5da057fb183dedfcd56e2 for more details.

## Updating the README.md File
* When the badges for your new project are ready, add the Markdown code for each integration badge to the README.md file.
* Enter the following commands:
```
git add .
git commit -m "Added continuous integration badges"
git push origin master
```
