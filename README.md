# Amahi Platform

[![Build Status](https://secure.travis-ci.org/amahi/platform.png)](http://travis-ci.org/amahi/platform) [![Code Climate](https://codeclimate.com/github/amahi/platform.png)](https://codeclimate.com/github/amahi/platform) [![Dependency Status](https://gemnasium.com/amahi/platform.png)](https://gemnasium.com/amahi/platform) [![Coverage Status](https://img.shields.io/coveralls/amahi/platform.svg)](https://coveralls.io/r/amahi/platform?branch=master)

The Amahi Platform is a web-based app that allows management of users, shares,
apps, networking and other settings in a Linux-based PC, VM or ARM-based system.

The Amahi Platform is part of Amahi and supports the services provided by [Amahi](http://www.amahi.org).

# Contributing

Contributions are always welcome! Here's what you need to do to get the Amahi platform working:

#### 1. Clone the repo

```bash
git clone https://github.com/amahi/platform.git
```

#### 2. Run the tests

You can test Amahi locally with limited functionality either on the command line or in the browser and both should work. Tests are written in CoffeeScript using [QUnit](http://docs.jquery.com/QUnit#API_documentation).

To run on the command line, run the following command from the project root:

```bash
make run-tests
```

#### 3. Write some test-driven code

The tests are in `spec/`. All test files are typically inside `spec/requests` and we use capybara and factory-girl for easy test writing.

#### 4. Test by hand in the browser

To run the app in the browser, you need to [bootstrap it](http://wiki.amahi.org/index.php/Amahi_Edge) first. The first DB: command assumes you have MySQL up and running and will ask for the root user credentials in MySQL:

```bash
bundle install
rake db:create
rake db:migrate
rake db:seed
```

To start the app and use it with a browser, start a web server with rails:

```bash
rails s
```

Visit `http://localhost:3000/`, login with the username of `admin` & the password of `secretpassword` and exercise the app as much as you can.

We like to follow a particular [git branching model](http://nvie.com/posts/a-successful-git-branching-model/). You can create and work in your own branch, making your work easier to track.

##### Install for Development Using docker
If you find it difficult to set up the development environment and all dependencies then you can use docker for an easy installation. Please note that docker and docker-compose must be installed on your system. 

For docker installation refer to the following link: https://docs.docker.com/engine/installation/
For docker-compose installation refer to the following link: https://docs.docker.com/compose/install/

Once that is done clone the code and go to the `config/database.yml` and put the following settings for development:
```yml
development:
  adapter: mysql2
  encoding: utf8
  pool: 5
  database: amahi_dev
  host: amahi_mysqldb
  username: root
  password: test123
```
Now run the following commands (Make sure you are at root directory of the code, docker-compose.yml file should be present in the directory) 
```sh
# Clone this code and go to the directory 
# Run bundle install to install all the required gems 
docker-compose run amahi_web bundle install
docker-compose run amahi_web rake db:create
docker-compose run amahi_web rake db:migrate
docker-compose run amahi_web rake db:seed
# As you can see, to run any rails command we have to just prepend the rails commands with "docker-compose run amahi_web" 
```
This should initialize everything required for the app. Now to run the server 
```sh
docker-compose up 
# or you can also do: "docker-compose run amahi_web rails s"
# You can do Ctrl+C to stop the server.
```
Running and creating migrations: 
```sh
# Running any rails command is fairly simple. You just have to prepend all the commands with: docker-compose run amahi_web
# Example: Generate a migration and run it.
docker-compose run amahi_web rails g migration addRandomStuff
docker-compose run amahi_web rake db:migrate

# Run a scaffold command
docker-compose run amahi_web rails g scaffold random
# Drop db 
docker-compose run amahi_web rake db:drop 
```
NOTE: The files generated by all the `rails` or `rake` commands might be owned by root and you might have to use `chown` to edit them. 

#### 5. Coding Style

Try to remove spurious white spaces and such. We have a [Ruby beautifier](https://github.com/amahi/rb-beautify) tool that we recommend. It's a basic ruby script that will modify any number of files (in the command line) to
make them more readable and keep the formatting conventions and styles that we like in Amahi.

#### 6. Create a pull request

When you are ready for your changes and it's good code that fits with the goals of the project, submit a pull request and we will merge it!

#### 7. Agree to CLA

For mutual protection, please check the icla.txt file for the individual contributor agreement we require for contributors. It's a virtual copy to Apache's CLA. Generally, you will be asked by email to read it and accept, otherwise it will be implied that you accept it. If you are working for a company or some large institution, we will ask that you submit a scan of the signed CLA for us to keep on file.

#### 8. Develop Plugins

We are trying to make the platform more modular and also thinner. If you have some ideas for plugins that
would improve the platform but are better done as plugins, See the [plugins](doc/plugins.md) docs file.

# License

This program is Copyright (C) 2007-2013, [Amahi](http://www.amahi.org).
Licensed under the AGPL. See the license in the [COPYING file](https://github.com/amahi/platform/blob/master/COPYING).
