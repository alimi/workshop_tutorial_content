{% header %}
  # 3 Viewing Data in the Browser
{% endheader %}

{% steps %}
  1.  You've added a lot of books to your bookstore, but wouldn't it be nice to
      actually see them in the browser? You are building a web application after
      all.

  1.  Before you can see your books, you'll need make some changes. Open the
      `bookstore` directory in your text editor.

  1.  Now open `config/routes.rb` and add the following line inside the only
      block in the file:

      ```
      resources :books
      ```

  1.  Save your changes.
{% endsteps %}

{% highlight ruby %}
  Rails.application.routes.draw do
    # For details on the DSL available within this file, see http://guides.rubyonrails.org/routing.html
    resources :books
  end
{% endhighlight %}

{% steps %}
  1.  Go back to Terminal and make sure you're in the `bookstore` directory.

  1.  Run `rake routes`. You should see a bunch of stuff about books along the
      lines of...

      ```
         Prefix Verb   URI Pattern               Controller#Action
          books GET    /books(.:format)          books#index
                POST   /books(.:format)          books#create
       new_book GET    /books/new(.:format)      books#new
      edit_book GET    /books/:id/edit(.:format) books#edit
           book GET    /books/:id(.:format)      books#show
                PATCH  /books/:id(.:format)      books#update
                PUT    /books/:id(.:format)      books#update
                DELETE /books/:id(.:format)      books#destroy
      ```

      `rake routes` prints a table of the available routes in your application.
      Since you added `books` as a resource in `config/routes.rb`, your
      application has a bunch of book routes.

      The `URI Pattern` column tells you how to reach the routes from a browser.

      For example, when your application is running locally you can reach
      `/books` by going to `http://localhost:300/books`.
{% endsteps %}

{% highlight shell %}
  › pwd
  /Users/awesomesauce/Projects/bookstore

  › rake routes
     Prefix Verb   URI Pattern               Controller#Action
      books GET    /books(.:format)          books#index
            POST   /books(.:format)          books#create
   new_book GET    /books/new(.:format)      books#new
  edit_book GET    /books/:id/edit(.:format) books#edit
       book GET    /books/:id(.:format)      books#show
            PATCH  /books/:id(.:format)      books#update
            PUT    /books/:id(.:format)      books#update
            DELETE /books/:id(.:format)      books#destroy
{% endhighlight %}

{% steps %}
  1.  Let's trying going to the `/books` route.

  1.  In Terminal, run `rails server` to start your application's web server.

  1.  Now, open your favorite web browser and go to
      [http://localhost:3000/books](http://localhost:3000/books).

  1.  If I had to guess, you probably got an error :)
{% endsteps %}

{% highlight shell %}
  › rails server
  => Booting Puma
  => Rails 5.0.0.1 application starting in development on http://localhost:3000
  => Run `rails server -h` for more startup options
  Puma starting in single mode...
  * Version 3.6.0 (ruby 2.3.1-p112), codename: Sleepy Sunday Serenity
  * Min threads: 5, max threads: 5
  * Environment: development
  * Listening on tcp://localhost:3000
  Use Ctrl-C to stop
  Started GET "/books" for ::1 at 2016-11-28 22:24:04 -0500
    ActiveRecord::SchemaMigration Load (0.4ms)  SELECT "schema_migrations".* FROM "schema_migrations"

  ActionController::RoutingError (uninitialized constant BooksController):
  ...
{% endhighlight %}

{% screenshot %}
  Routing Error
  uninitialized constant BooksController
{% endscreenshot %}

{% steps %}
  1.  We've run into a problem, but Rails is giving us some info to help us
      understand what's going on.

      You're getting a `Routing Error` because there's an `uninitialized
      constant BooksController`. Rails is expecting your application will have a
      `BooksController`, so let's create it!

  1.  Stop your rails server by running `Ctrl-c`.

  1.  Create the `BooksController` by running
      `touch app/controllers/books_controller.rb`.

  1.  Restart your web server by running `rails server`, and try going to
      [http:://localhost:3000/books](http:://localhost:3000/books) again.

      That still errored, didn't it? But hey, at least you got a new error!
{% endsteps %}

{% highlight shell %}
  › rails server
  => Booting Puma
  => Rails 5.0.0.1 application starting in development on http://localhost:3000
  => Run `rails server -h` for more startup options
  Puma starting in single mode...
  * Version 3.6.0 (ruby 2.3.1-p112), codename: Sleepy Sunday Serenity
  * Min threads: 5, max threads: 5
  * Environment: development
  * Listening on tcp://localhost:3000
  Use Ctrl-C to stop
  ...
  ^CExiting

  › touch app/controllers/books_controller.rb

  › rails server
  => Booting Puma
  => Rails 5.0.0.1 application starting in development on http://localhost:3000
  ...
  Use Ctrl-C to stop
  Started GET "/books" for ::1 at 2016-11-29 20:55:26 -0500
    ActiveRecord::SchemaMigration Load (0.2ms)  SELECT "schema_migrations".* FROM "schema_migrations"

  LoadError (Unable to autoload constant BooksController, expected /Users/awesomesauce/Projects/bookstore/app/controllers/books_controller.rb to define it):
{% endhighlight %}

{% screenshot %}
  LoadError in BooksController#index
  Unable to autoload constant BooksController, expected /Users/awesomesauce/Projects/bookstore/app/controllers/books_controller.rb to define it
{% endscreenshot %}

{% steps %}
  1.  Now you got a `LoadError` because `BooksController` isn't defined.

      ```
      Unable to autoload constant BooksController, expected
      /Users/awesomesauce/Projects/bookstore/app/controllers/books_controller.rb
      to define it
      ```

  1.  Remember the `touch` command we used to create the `BooksController`?

      `touch app/controllers/books_controller.rb`.

      It created the `BooksController` file, but the file is empty. Don't belive
      me? Let's take a look.
{% endsteps %}

{% steps %}
  1.  If you're text editor isn't already open, open it and go to the
      `bookstore` directory.

  1.  Now, open `app/controllers/books_controller.rb`.

  1.  See, it's empty :)

      `touch` creates empty files. We used it to create an empty file called
      `app/controllers/books_controller.rb`.

  1.  The error you got said something about there being a missing constant
      `BooksController`. Let's add it.

  1.  Add the following code to `app/controllers/books_controller.rb`:

      ```
      class BooksController < ApplicationController
      end
      ```

      That should define the constant Rails was looking for.

  1.  Save the file and try going to
      [http://localhost:3000/books](http://localhost:3000/books) again.

      New error!
{% endsteps %}

{% highlight ruby %}
  class BooksController < ApplicationController
  end
{% endhighlight %}

{% screenshot %}
  Unknown action
  The action 'index' could not be found for BooksController
{% endscreenshot %}

{% steps %}
  1.  This new error is telling us that you're `BooksController` doesn't have an
      `index` action. That kinda makes sense - we didn't add very much code to
      the `BooksController`. But why does it care that the `index` action is
      missing?

  1.  Remember the routing table? Kinda? Don't worry, it's fuzzy for me too.
      Let's pull it up again.

  1.  Go back to Terminal and stop the `rails server` by running `Ctrl-c`.

  1.  Now, run `rake routes`. Voila - the routing table.

  1.  The first entry in the routing table is for the `/books` path.

      ```
      Prefix Verb   URI Pattern               Controller#Action
       books GET    /books(.:format)          books#index
      ```

      The last column tells us which controller and action get run when we go to
      the `/books` path.

      The URI Pattern `/books(.:format)` maps to the Controller#Action pair of
      `books#index`. This tells us requests to the `/books` path will be routed
      to the `BooksController` `index` action.

      Clear as mud, right? Don't worry, it'll make more sense later.

  1.  Now that we (kinda) know why we're trying to run the `index` action`,
      let's add it.

  1.  Before we go on, restart your web server by running `rails server`.
{% endsteps %}

{% highlight shell %}
  › rails server
  => Booting Puma
  ...
  ^CExiting

  › rake routes
     Prefix Verb   URI Pattern               Controller#Action
      books GET    /books(.:format)          books#index
            POST   /books(.:format)          books#create
   new_book GET    /books/new(.:format)      books#new
  edit_book GET    /books/:id/edit(.:format) books#edit
       book GET    /books/:id(.:format)      books#show
            PATCH  /books/:id(.:format)      books#update
            PUT    /books/:id(.:format)      books#update
            DELETE /books/:id(.:format)      books#destroy

  › rails server
  => Booting Puma
  ...
{% endhighlight %}

{% steps %}
  1.  In your text editor, open the `BooksController` and add the following
      method inside the `BooksController` class.

      ```
      def index
      end
      ```

  1.  Save your changes and try going to
      [http://localhost:3000/books](http://localhost:3000) again.

      ![Aaugh!](http://25.media.tumblr.com/tumblr_lz8plpLwB11qg39ewo1_500.gif)
{% endsteps %}

{% highlight ruby %}
  class BooksController < ApplicationController
    def index
    end
  end
{% endhighlight %}

{% screenshot %}
  ActionController::UnknownFormat in BooksController#index
  BooksController#index is missing a template for this request format and variant.
{% endscreenshot %}

{% steps %}
  1.  We're making progress. Seriously! The `/books` path is sucessfully
      reaching the `BooksController` `index` action, but we're getting an error
      because we're missing a template.

      A template is a view that get's rendered at the end of a controller
      action. In this case, Rails is expecting your applicaiton to have an
      `index` template to go with the `BooksController` `index` action.

      Let's make that happen!

  1.  Stop your `rails server` by running `Ctrl-c`.

  1.  All templates live in `app/views`.

      `app/views` will have directories for each of the controllers in your
      application. By default, a controller's template directory will be the
      name of the controller...minus the controller.

      For example, the `BooksController`'s template directory will be
      `app/views/books`.

  1.  Create the `BooksController` template directory by running `mkdir
      app/views/books`.

  1.  Now, create the `BooksController`'s `index` template by running `touch
      app/views/books/index.html.erb`.`

  1.  Restart your web server.

      (Remember? Start your web server by running `rails server`.)

  1.  Now, try going to
      [http://localhost:3000/books](http://localhost:3000/books).

      Yay, no errors!
{% endsteps %}

{% highlight ruby %}
  › rails server
  => Booting Puma
  ...
  ^CExiting

  › mkdir app/views/books

  › touch app/views/books/index.html.erb

  › rails server
  ...
  Started GET "/books" for ::1 at 2016-11-29 22:15:07 -0500
    ActiveRecord::SchemaMigration Load (0.2ms)  SELECT "schema_migrations".* FROM "schema_migrations"
  Processing by BooksController#index as HTML
    Rendering books/index.html.erb within layouts/application
    Rendered books/index.html.erb within layouts/application (1.7ms)
  Completed 200 OK in 645ms (Views: 631.6ms | ActiveRecord: 0.0ms)
{% endhighlight %}
