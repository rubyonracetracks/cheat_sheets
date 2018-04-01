# Reset Your Rails Development Environment

## Prerequisites
It is assumed here that your Rails app has been created with the GenericApp gem and that you are using Docker for your development environment.

## Procedure
* Make sure that your Git repository for this project is up to date.
* Go to the tmux window dedicated to the local Rails server. Press Ctrl-C to stop the server. When it has stopped, enter "exit" to exit tmux.
* In your Docker container, go to the tmux window for entering commands and enter "exit". This gets rid of that tmux window.
* If you have any other tmux windows open, get rid of those as well.
* Enter "exit" again to leave the Docker container. You should now be back in the host environment.
* Enter the command "sh reset.sh" to reset the Docker container to its initial conditions.
* Delete the local version of your project's source code.
* Git clone the project's source code.
* Start tmux.
* Enter your app's root directory.
* Enter the command "sh credentials.sh". (NOTE: If you are not using Heroku, remove the Heroku section in this script.)
* Enter the command "sh build_fast.sh; sh server.sh". Open your web browser to the appropriate URL to view your app locally. (NOTE: The build_fast.sh script takes a few minutes to test your app, outline your app, and seed the database.)
* Start a second tmux window, and go to your new app's root directory. Use this tmux window for entering commands.
