# Post Rails Neutrino To Do List

This document covers the tasks you should do after using Rails Neutrino to start a new Ruby on Rails project.

## Getting Started
* Start tmux.  Go to your new app's root directory.
* Enter your new app's root directory.
* Enter the command "sh build_fast.sh; sh server.sh".  Open your web browser to the appropriate URL to view your app locally.  (NOTE: The build_fast.sh script takes a few minutes to test your app, outline your app, and seed the database.)  
* Start a second tmux window, and go to your app's root directory.  Use this tmux window for entering commands.
* Start a Git repository for your new app, and push your new app into that repository.
* Deploy this app.  Instructions for deploying to Heroku are at https://github.com/rubyonracetracks/cheat_sheets/blob/master/rails_heroku.md .
* Add continuous integration badges to your README.md page.  Instructions are at https://github.com/rubyonracetracks/cheat_sheets/blob/master/continuous_integration.md .
* If all goes well, the new app is ready to be used by the [Generic App gem](https://github.com/rubyonracetracks/generic_app).

## Updating Generic App
* Download the [Generic App source code](https://github.com/rubyonracetracks/generic_app).
* Edit the file generic_app/lib/generic_app/version.rb and update the version number.
* Edit the file generic_app/lib/generic_app.rb and update the value of the variable URL_TEMPLATE (defined at the beginning).
* In the terminal, go to the root directory of generic_app.  Test the gem by entering the command "sh all.sh".  All tests should pass, there should be no RuboCop offenses, and the Rails Neutrino timestamp of your new app should correspond to that of the app you created.
* Test the gem AND the app it creates by entering the command "sh long_test.sh".  All tests should pass, there should be no RuboCop offenses, and the Rails Neutrino timestamp of your new app should correspond to that of the app you created.
* If all goes well, you are ready to commit the source code and publish the next version of the gem.
