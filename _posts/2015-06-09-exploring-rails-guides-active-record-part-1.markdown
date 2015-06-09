---
title:  "Exploring Rails Guides - Active Record - Part 1"
---

At [Genii](http://genii.in), we had a tradition; Every new developer would have to go through the [Rails Guides](http://guides.rubyonrails.org/) before he was assigned to a project. I did that too. Being new to Rails and professional development I found it a bit overwhelming. I had decided that I would revisit Rails Guides in a few months but kept postponing it. Now that I have time, I decided to go through all the Rails Guides and document interesting stuff. Let's start with ActiveRecord.


Reserved Column Names
----------------------
We all are aware of `created_at` and `updated_at`. Almost every table in a Rails app has these columns. But there are 4 other [column names reserved by ActiveRecord](http://guides.rubyonrails.org/active_record_basics.html#schema-conventions). While having them in you models doesn't necessarily break the application, It is advised to steer clear of reserved keywords in case you need that functionality in the future.


Overriding Table Name and Primary Key
--------------------------------------
By default, ActiveRecord considers `id` column as primary key and table name will be lower case pluralized version of the model name. But it's easy to override these defaults. This is particularly useful if you are using a legacy or 3rd party database.


reversible block in Migrations
-------------------------------
You can specify migrations in change method. And if they can't be auto reversed by Rails, you can use up and down method. This is a bit cumbersome if only one statement in your migration is not auto-reversible. You end up writing up and down migrations for all the other statements. You can avoid this by using [reversible](http://guides.rubyonrails.org/active_record_migrations.html#using-reversible) block inside change method.


Reverting Previous Migrations
------------------------------
If you want to revert an old migration or part of it, [revert](http://guides.rubyonrails.org/active_record_migrations.html#reverting-previous-migrations) method is the way to go. You can pass class of the migration you want to revert and ActiveRecord will take care of it. The `revert` method also accepts a block which you can use to revert part of a previous migration.


SQL Schema Dumping
-------------------
By default, ActiveRecord stores structure of the database in `db/schema.rb`. This file is updated every time you run a migration. ActiveRecord uses schema file to recreate db structure when you run `db:setup` or `db:reset`. But if you have specified database specific items such as triggers, or stored procedures these are not reflected in schema.rb. In such cases you can change schema type to [SQL](http://guides.rubyonrails.org/active_record_migrations.html#types-of-schema-dumps).

When you set this  option, instead of using Active Record's schema dumper, the database's structure will be dumped using a tool specific to the database (via the `db:structure:dump` Rake task) into `db/structure.sql`. For example, for PostgreSQL, the pg_dump utility is used. For MySQL, this file will contain the output of SHOW CREATE TABLE for the various tables. Using the `:sql` schema format will, however, prevent loading the schema into a RDBMS other than the one used to create it.


Callback Chain
---------------
When you add new [callbacks](http://guides.rubyonrails.org/active_record_callbacks.html#available-callbacks) to your models, they are added to an execution chain along with validations and database operations. The whole chain is wrapped in a transaction. If any before callback method returns exactly false or raises an exception, the execution chain gets halted and a ROLLBACK is issued; after callbacks can only accomplish that by raising an exception.


after_save vs after_commit
---------------------------
Rails calls `after_save` callbacks immediately after the record saves. But that record can't be seen by other database connections, until the database transaction is committed. `after_commit` callbacks are run when database transaction has been committed. They are not interchangeable and using them involves some interesting [gotchas](http://www.justinweiss.com/blog/2015/03/10/a-couple-callback-gotchas-and-a-rails-5-fix/).


Callback Classes
-----------------
If two or more models share the same callback code, it's easy to DRY them up by using [Callback Classes](http://guides.rubyonrails.org/active_record_callbacks.html#callback-classes). You could also use [Concerns](https://signalvnoise.com/posts/3372-put-chubby-models-on-a-diet-with-concerns) for DRYing up models. But Callback Classes seem cleaner if only callback code is repeated.


That's it for now. So far I have covered Migrations, Validations and Callbacks. Will cover the rest of the ActiveRecord in the next post.
