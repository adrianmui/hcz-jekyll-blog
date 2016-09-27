---
layout: post
title:  "Week 11: Guide to Rails APP"
date:   2016-09-25 00:00:00 -0400
categories: vcs
---

*(in progress)*

# Getting Started on a Rails Project

It's always hard getting started on a project. You don't really know where to begin. There's a million things to setup. What are those things? You don't really know. It's been awhile since you last started your own project. Well, since I'm in the process of doing that myself, I might as well write about it.

Here are a few things I've decided for the project layout:

* Coded in Ruby using Rails Framework
* To be Setup in PostgreSQL for Heroku-Deployment
* Devise Authentication (User/Password Confirm, Salted Passwords)
* Sendgrid + Delayed Jobs (email confirms, working dynos)
* (Optional) AWS + Paperclip, storing images over Amazon Server
* (Optional) Seeds to unload on empty database
* (Semi-Optional) Unit Testing with Rspec, Shoulda, and FactoryGirl
* (Situational) Figaro for private API keys in ENV file
* Bootstrap - Intuitive Interface is a **MUST**.
* git, git, git started.

## Starting Point

Creating your repository on github. I personally like to do it from Github's web interface. Type this in your terminal.

```
git clone https://github.com/username/your_repo.git
```
Edit your readme. include your name, maybe a description of your project. Commit. Push.

```
git commit -a -m "initial commit, edit readme.txt"
git push
```

<h2>Setting up Rails with postgreSQL</h2>

If you intend on deploying to Heroku, make sure to start the database with postgreSQL. If not, prepare yourself for heaps of heroku/deploy bugs later on.

```
rails new ~/directory/myApp --database=postgresql
```

<h2>API, Figaro </h2>

If you intend on accessing private apis, you need to keep your api keys and ids in a safe place. One way of keeping your 'secrets' safe is by using environment variables. To do this, it's best to use the figaro gem.

In your Gemfile, include:

```
gem figaro
```
In your Console:

```
bundle install
bundle exec figaro install (this creates your application.yml and adds it to .gitignore, which ignores the file when commiting to github)
```

In your application.yml, store your variable keys:

```
  SUPER_SECRET_API_KEY: "1234567HARAMBE89"
```
Make sure your secrets.yml is doing the same:

```
  production/development do:
    SUPER_SECRET_API_KEY: <%= ENV["SUPER_SECRET_API_KEY"] %>
```

Now, whenever you'd like you can access the key with ```Rails.applications.secrets.SUPER_SECRET_API_KEY```



