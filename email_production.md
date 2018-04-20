# Enabling Email in the Production Environment of Your New Rails App

When you use the GenericApp gem, the email functions work in the development and testing environment but NOT in the production environment.  For the production environment, each individual Rails app has a custom configuration.

## Lists of Production Email Providers
  * [List (from RailsApps)](http://railsapps.github.io/rails-send-email.html)
  * [List (from Chris Hager)](https://www.metachris.com/2016/03/free-transactional-email-services-the-best-alternatives-to-mandrill/)
  * [turboSMTP](http://www.serversmtp.com/): up to 6000 free emails per month
  * [Mailgun](http://www.mailgun.com/): up to 10,000 free emails per month
  * [SparkPost](https://www.sparkpost.com/): up to 100,000 free emails per month
  * [Elastic Email](https://elasticemail.com/): up to 150,000 free emails per month
  * [SendGrid](http://sendgrid.com/): free 30-day trial of up to 40,000 emails
  * [MailJet](https://www.mailjet.com/): free 1-month trial of up to 6000 emails (up to 200 per day)
  
## Procedures
* [Heroku/SendGrid](https://github.com/rubyonracetracks/cheat_sheets/blob/master/heroku_email/heroku_sendgrid.md)
* [Heroku/Mailgun](https://github.com/rubyonracetracks/cheat_sheets/blob/master/heroku_email/heroku_mailgun.md)
* [Heroku/SparkPost](https://github.com/rubyonracetracks/cheat_sheets/blob/master/heroku_email/heroku_sparkpost.md)
