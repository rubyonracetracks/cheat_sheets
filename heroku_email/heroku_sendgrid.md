# Heroku/SendGrid

This document explains how to use SendGrid to provide email capabilities for a Ruby on Rails app deployed to Heroku.  NOTE: SendGrid's free service is a 30-day trial.

## Prerequisites
It is assumed here that you have created your app, pushed it to a Git repository, and deployed it to Heroku.

## Links
* The best procedure is from [Brian Arpaio's blog](http://www.rpayo.com/2016/11/20/rails-sending-automated-emails-with-devise-and-sendgrid-on-heroku/).  I was confused by the documentation from Heroku and SendGrid.
* [SendGrid](http://sendgrid.com/): free 30-day trial of up to 40,000 emails  

## Procedure
* Log into your account at [SendGrid](http://sendgrid.com/).  If you don't already have an account, create one.  You can start off with the free tier of service.
* Go to the [API Keys page](https://app.sendgrid.com/settings/api_keys) in SendGrid.
* Click on the "Create API Key" button, and then select the "General API Key" option.
* Select the "full access" option for as many functions as possible.  When the "full access" option is not available, select the "read access" option.
* When you are given your API key, save it IMMEDIATELY in KeePassX.
* Log into your Heroku account.  In your Dashboard, select your new Rails project, and click on "Configure Add-ons".
* Go to the Add-ons section, enter "SendGrid", pick the appropriate SendGrid plan, and click on "Provision".
* In the command line, enter the following command:
```
heroku config:set SENDGRID_API_KEY='(fill in your API key here)'
```
* View your app's username and password by entering "heroku config".
* Edit the config/environments/production.rb file, and add the new custom production email settings to the end of the configuration settings.  It should look like this:
```
  . . . .

  config.action_mailer.default_url_options = { host: 'your_app.herokuapp.com' }
  ActionMailer::Base.smtp_settings = {
    address: 'smtp.sendgrid.net',
    port: '25',
    authentication: :plain,
    user_name: ENV['SENDGRID_USERNAME'],
    password: ENV['SENDGRID_PASSWORD'],
    domain: ENV['SENDGRID_DOMAIN']
  }
end
```
* In the config/environments/production.rb file, replace "your_app" in the config.action_mailer.default_url_options with the actual name in the URL of your Heroku app.
* Add the following line to the very beginning of config/environments/production.rb:
```
# rubocop:disable Metrics/BlockLength
```
* Add the following line to the very end of config/environments/production.rb:
```
# rubocop:enable Metrics/BlockLength
```
* Enter the command "sh git_check.sh".  All tests should pass, and there should be no offenses.
* Enter the following commands:
```
git add .
git commit -m "Enabled emails in Heroku through SendGrid"
git push origin master
sh heroku.sh
```
* Go to your app's Heroku page, and sign up for a new account.  The email confirmation processes should now work.
