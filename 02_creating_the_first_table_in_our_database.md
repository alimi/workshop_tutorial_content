{% header %}
  # 2 Creating the First Table in Our Database
{% endheader %}

{% steps %}
  1.  Open Terminal and `cd` to `Projects/bookstore` from your home directory.

      If you have Terminal open from the previous chapter, you should already be
      in `HOME/Projects/bookstore`. Remember how to check what directory you're
      in?

      (`pwd`)

  1.  Run `rails generate model book`.

      This generated a few files, but there are only a couple we're interesed
      in.

  1.  Run `ls -l db/migrate`. You should see a file named something like
      `20161115030350_create_books.rb`.

      20161115030350 is a timestamp generated when the file is created. You're
      file will start with a more recent timestamp...I hope :)

      Let's take a look at this file in your text editor.
{% endsteps %}

{% highlight %}
  › pwd
  /Users/awesomesauce/Projects/bookstore

  › rails generate model book
        invoke  active_record
        create    db/migrate/20161115030350_create_books.rb
        create    app/models/book.rb
        invoke    test_unit
        create      test/models/book_test.rb
        create      test/fixtures/books.yml

  › ls -l db/migrate
  total 8
  -rw-r--r--  1 alimi  staff  131 Nov 14 22:03 20161115030350_create_books.rb
{% endhighlight %}

{% steps %}
  1.  Open the `bookstore` directory in your text editor and open
      `db/migrate/YOUR_TIMESTAMP_create_books.rb`.

  1.  This is a migration file called `CreateBooks`. Migrations are used to
      make changes to the database.

  1.  On line 3 of the `CreateBooks` migration, there's a block called
      `create_table`. Inside this block, you'll make changes to add columns to
      the new `books` table.
{% endsteps %}

{% highlight ruby %}
  class CreateBooks < ActiveRecord::Migration[5.0]
    def change
      create_table :books do |t|

        t.timestamps
      end
    end
  end
{% endhighlight %}

{% steps %}
  1.  The `books` table will need a few columns.

      It will need a string column to store book titles and another string
      column to store book authors.

      The table will also need a column to store book prices. Since keeping
      track of money can be tricky, the column will need to be an integer where
      book prices can be stored in cents. It sounds weird, but you'll have to
      trust us on this one.

  1.  After line 3 of the `CreateBooks` migration, add the following:

      ```
      t.string :title
      t.string :author
      t.integer :price_cents
      ```

  1.  You've added a few things to the `create_table` block, but you might've
      noticed that there was already some code in there:

      ```
      t.timestamps
      ```

      What's t.timestamps doing? It's a convinence method added by Rails that
      will add two more columns to the `books` table: `created_at` and
      `updated_at`. They'll be used to store the time when books are created and
      updated.

  1.  Save your changes to the `CreateBooks` migration and go back to Terminal.
{% endsteps %}

{% highlight ruby %}
  class CreateBooks < ActiveRecord::Migration[5.0]
    def change
      create_table :books do |t|
        t.string :title
        t.string :author
        t.integer :price_cents
        t.timestamps
      end
    end
  end
{% endhighlight %}

{% steps %}
  1.  In Terminal, make sure you're in the `bookstore` directory.

  1.  Run `rake db:migrate`.

  1.  Yay! You've just run your first migration!
{% endsteps %}

{% highlight %}
  › pwd
  /Users/awesomesauce/Projects/bookstore

  › rake db:migrate
  == 20161115030350 CreateBooks: migrating ======================================
  -- create_table(:books)
     -> 0.0030s
  == 20161115030350 CreateBooks: migrated (0.0034s) =============================
{% endhighlight %}
