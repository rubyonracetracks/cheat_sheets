# Heroku/SparkPost
This document explains how to implement SparkPost's production email service for your Rails app on Heroku.

## SPECIAL NOTE
Heroku no longer offers a free plan for using SparkPost.  If you don't want to pay, the Heroku/SparkPost combination is not for you.

## Prerequisites
* You have created a Rails app that uses authentication and deployed it to Heroku.
* You need an account at [SparkPost](https://www.sparkpost.com/).
* You must have an API key.  Log into SparkPost, go to Account -> API Keys, create a new API key, and SAVE your API key to KeePassX (or other password manager).  Be sure to enable (check) the "Send via SMTP" API permission.
* You must have a valid sending domain.  Log into SparkPost, go to Account -> Sending Domains, and create a new domain.  The email address you use as the source of the email confirmation messages (which is set in the config.mailer_sender parameter in the config/initializers/devise.rb file) MUST be part of one of your sending domains.  Additionally, you must verify your sending domain through either the DKIM record or email confirmation.

## Troubleshooting
* If the email confirmation process doesn't work (and leaves you with the message "We're sorry, but something went wrong."), you need to view your Heroku app's log to see the error message.
* The number of lines shown when you type "heroku logs" is limited.  You may need to type "heroku logs -n5000" or "heroku logs --tail" to see the source of your error.

## Procedure
* Log into your Heroku account.  In your Dashboard, select your new Rails project, and click on "Configure Add-ons".
* Go to the Add-ons section, enter "SparkPost", pick the appropriate SparkPost plan name, and click on "Provision".
* In the command line, enter the command "heroku config" to verify that your app is configured for SparkPost on Heroku.
* Log into your SparkPost account.  Go to Account -> SMTP Relays for the values of the host, username, and password parameters.  Please note that the password is your API key.
* Go to your app's Settings page on the Heroku web site, and change certain config variables.  (Some of the default parameters are wrong.)  The SPARKPOST_API_KEY, SPARKPOST_SMTP_PORT, SPARKPOST_SMTP_USERNAME, SPARKPOST_SMTP_PASSWORD, and SPARKPOST_SMTP_PORT parameters in the Heroku app need to match the values listed in the SMTP Relays page of the SparkPost site.
* Edit the config/environments/production.rb file, and add the new custom production email settings to the end of the configuration settings.  (Replace "your_app" with the actual name of your app on Heroku.)  It should look like this:
```
  . . . .

  # SparkPost settings
  config.action_mailer.default_url_options = { host: 'yourapp.herokuapp.com' }
  config.action_mailer.smtp_settings = {
    port: ENV['SPARKPOST_SMTP_PORT'],
    address: ENV['SPARKPOST_SMTP_HOST'],
    user_name: ENV['SPARKPOST_SMTP_USERNAME'],
    password: ENV['SPARKPOST_SMTP_PASSWORD'],
    domain: 'yourapp.heroku.com',
    authentication: :plain
  }
  config.action_mailer.delivery_method = :smtp
end
```
* In the config/environments/production.rb file, replace BOTH instances of "yourapp" in the above file with the actual name within the URL of your Heroku app.
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
git commit -m "Configured production settings for SparkPost"
git push origin master
sh heroku.sh
```
* Go to your app's Heroku page, and sign up for a new account.  The email confirmation processes should now work.
