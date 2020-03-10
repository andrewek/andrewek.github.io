---
layout: post
title: "A Reasonably Pleasant Wordpress Setup with Docker"
video: false
image: bee.jpg
categories: [docker, wordpress, development-environment]
---

I recently had to help a customer troubleshoot a Wordpress setup. This isn't a
big deal, but it'd been long enough since the last time I had Wordpress running
locally that I couldn't remember the exact steps for getting MAMP, PHPMyAdmin,
and the like running to actually get the site up.

We've been using Docker (and docker-compose) at work quite a bit, so I sought
out a docker container that handled much of that setup for me.

As it turns out, the fine folks at Docker [already have a
guide](https://docs.docker.com/compose/wordpress/).

The issue we came across is that while we can get Wordpress running, we can't
hack on it (notably, custom theme or plugin development).

So let's resolve this. I'm assuming here that you're fairly comfortable with
Wordpress itself, and perhaps somewhat comfortable with Docker and
Docker-Compose. I'm also assuming you've got Docker for Mac (or the equivalent
for your platform) installed. I'm also assuming here that you're relatively
comfortable with your terminal (everything here assumes a \*nix shell, like
what you'd find if you're using Linux or a Mac).

Let's begin. We're going to create a relatively pleasant setup where we can have
our wordpress site running and where we can spin it up (and tear it down) as we
desire.

(If you feel like skipping to the good stuff, all of our work below, genericized
just a bit, [can be found
here](https://github.com/andrewek/docker-wordpress-demo))

First, let's make some room:

{% highlight shell %}
$ mkdir wordpress_sites
$ cd wordpress_sites
{% endhighlight %}

Then we'll create a file for our docker-compose setup, but we won't put anything
in it just yet (we will soon).

{% highlight shell %}
$ touch docker-compose.yml
{% endhighlight %}

Finally, we'll get setup with Git (if you don't yet use Git, don't worry about
this step):

{% highlight shell %}
$ git init .
$ touch .gitignore
{% endhighlight %}

Your `.gitignore` file should look like this (again, ignore this if you aren't
using Git):

{% highlight text %}
look_a_dog/
{% endhighlight %}

Now we can get started on our actual docker-compose file, which we'll use to
orchestrate this whole process:

{% highlight yaml %}

version: '3.3'

services:
  look_a_dog_wp:
    # We need a database
    depends_on:
      - db
    # We'll use the most recent Wordpress install
    image: wordpress:latest
    # We're going to stick all of our files in our
    # look_a_dog directory; this keeps it nice and separate
    # from our other sites (if applicable).
    volumes:
      - ./look_a_dog:/var/www/html
    ports:
    # We'll access our site on http://localhost:8999
      - "8999:80"
    restart: always
    environment:
      # We'll provide some SQL credentials -- these match what's
      # in our db section
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress

  # This is our MySQL database server
  db:
    image: mysql:5.7
    # We need a volume here, too, otherwise all of our posts
    # and users will disappear whenever we stop our server.
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    # We'll set root DB credentials
    environment:
      MYSQL_ROOT_PASSWORD: somewordpress
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress
volumes:
  db_data:

{% endhighlight %}

We've got our Docker-Compose file set up, so now we can run it:

{% highlight shell %}
$ docker-compose up
{% endhighlight %}

We should see a bunch of output (this process will take a few minutes). Once the
output generally stops (assuming no error messages), you can do two things:

1. Navigate your fine self to `http://localhost:8999` -- you'll be prompted to
   finish setup
2. Take a look inside your `look_a_dog` folder -- you should see all of your
   normal Wordpress files (this folder previously did not even exist!). You'll
   note that this is also the folder we git-ignored, so as to keep any updates
   here from affecting our base playground.

You can stop the containers with `CTRL-C`, and you can tear the whole thing down
with `docker-compose down` (or delete it entirely with `docker system prune` and
`docker volume prune`).

If you're not using Git, you can proceed here exactly as you would normally.
Updates inside the local folder are reflected on the Docker container, and
vice-versa.

If you are using Git, what I'll suggest is to get individual folders (for
example, if you're making a new theme, the folder containing that theme, e.g.
`wp-content/themes/dog_theme`) under version control. You've already git-ignored
the whole site directory, so you shouldn't run into the strange set of maladies
that come from having git repositories inside of git repositories, and you'll be
able to better collaborate with others.

Ultimately, what this gives you is a base wordpress install that you can freely
hack on without the muss or fuss of working with MAMP/WAMP and running things
locally.
