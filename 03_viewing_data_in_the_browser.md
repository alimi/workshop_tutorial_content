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
{% endsteps %}
