{% section_header %}
  # 1 Getting Started from Scratch
{% endsection_header %}

{% protip %}
  Throughout the tutorial, we're going to run a lot of Terminal commands. For
  example, we might ask you to do something like

  > Run `pwd` to print your current working directory.

  To run the command, you'll need to type it in Terminal and hit `enter` to
  execute it.
{% endprotip%}

{% steps %}
  1.  Open Terminal.

  1.  You're now in your home directory. Run `ls` to see what's in your home
      directory. You might see some familiar directories like `Desktop`,
      `Documents`, and `Music`.

  1.  All code deserves a good home. Add a new `Projects` directory to your home
      directory by running `mkdir Projects`.

  1.  Navigate to your new `Projects` directory by running `cd Projects`.

  1.  Now you're ready to create the bookstore!
{% endsteps %}

{% highlight %}
  > ls
  Desktop Document Music

  > mkdir Projects

  > cd Projects
{% endhighlight %}

{% protip %}
  Before you can complete the following steps, your computer needs to be
  configured with Rails. If you haven't already, please refer to the [install
  instructions](link) for steps on configuring your computer.
{% endprotip %}

{% steps %}
  1.  In your `Projects` directory, run `rails new bookstore`.

  1.  `rails new` does a lot of stuff! First, it creates the files and
      directories that make up the basic structure of your bookstore
      application. Then, it runs `bundle install` to install the dependencies
      needed to run the application.

  1.  After `rails new` finishes, run `cd bookstore` to navigate to the newly
      created bookstore application.
{% endsteps %}

{% highlight %}
> rails new bookstore
      create
      create  README.md
      create  Rakefile
      create  config.ru
      create  .gitignore
      create  Gemfile
      create  app
      ...
      run bundle install
Fetching gem metadata from http://rubygems.org/...........
Fetching version metadata from http://rubygems.org/...
Fetching dependency metadata from http://rubygems.org/..
Resolving dependencies..................
Installing rake 11.3.0
...
{% endhighlight %}
