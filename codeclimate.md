# Code Climate Setup

Code Climate has great tools.  Unfortunately, the instructions are incomplete.

## Log In and Track Your Project
* Go to the [Code Climate web site](https://codeclimate.com/).
* If you haven't already done so, create an account.
* Log into your account.
* Select your project as one to follow.
* If projects from your GitHub organization are not listed, go to https://docs.codeclimate.com/docs/approve-code-climate-as-a-third-party-application-in-github-1.

## Badge Location
Your project's badges are located at https://codeclimate.com/github/your_github_username/your_project_name/badges.

## GPA Rating
Getting the GPA Rating is a relatively straightforward process, and additional instructions are not necessary.

## Test Coverage Percentage
* I recommend measuring and posting test coverage percentage for Ruby gems but NOT for Rails apps.  (In Rails apps, I found that SimpleCov failed to evaluate certain parts of the source code or showed tested code to be untested.)
* There are several elements that you MUST have in place:
  * Your app must be tested by a continuous integration service like Travis, CircleCI, etc.
  * The simplecov and codeclimate-test-reporter gems must be specified for the development environment in the Gemfile (for a Rails app) or in the *.gemspec file (for a Ruby gem project).
  * The spec/spec_helper.rb file (if you're using Rspec) or test/test_helper.rb file (if you're using Minitest) must have the following lines in place AT THE BEGINNING in order to start SimpleCov:
```
require 'simplecov'
SimpleCov.start
```
  * If you are using Travis CI, the .travis.yml file should have the following lines to prompt Travis CI to automatically run the CodeClimate test reporter after each test:
```
after_success:
  - bundle exec codeclimate-test-reporter
```
  * In your continous integration testing service, you must configure your project to run the Code Climate Test Reporter after running all tests.  For example, if you are using CircleCI, go to your project's settings in CircleCI, and add the following command to the post-test commands to automatically run the CodeClimate test reporter after each test:
```
bundle exec codeclimate-test-reporter
```
  * Get your project's CODECLIMATE_REPO_TOKEN.  Go to your project's CodeClimate page, click on "Settings", and then click on "Test Coverage".  Get the Test Reporter ID, which you will use as the value of the environment variable CODECLIMATE_REPO_TOKEN.
  * Go to your project in Travis CI, CircleCI, Semaphore CI, etc., and add the environment variable CODECLIMATE_REPO_TOKEN set to the appropriate value.
