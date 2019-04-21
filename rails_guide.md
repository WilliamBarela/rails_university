# Rails Guide

## What is an Ruby on Rails?

Ruby on Rails is a **Model** **View** **Controller** (MVC) framework which is very powerful and values convention over configuration.
MVC is a common pattern for web applications and seeks to ensure separtation of concerns within the code base.
In addition to this, there are also several other features which make it easy for a developer to quickly build out a web application.
Rails can be very feature filled and allows for several other classes including a testing framework, mailers, and storage classes.

## What is an MVC? How does it connect to the database?

### Migrations
A web application without persistance in a database can only be classed as little more than a front-end.
As a result, one could write SQL to connect to the database and persist these values; however, that is brittle as it locks you into the SQL specification of one given database.
Thus, Rails also has migration classes which are stored in `$YOUR_RAILS_APP_DIR/db/migrations`.
Migrations are Ruby classes as well which inherit from the `ActiveRecord::Migration` class.
They are an **ORM** (objection relationship mapping) which allows for database independance (Rails is open source and many people have worked hard to include the SQL equivalent across several different RDBMS'.)
Migration classes specify which fields to add to which tables and what datatype they should be classed as.
Migrations also act as something of a version control system which you can use to communication from Rails to your database and go back to a previous moment in the databases development.
In sum, migrations allow your Rails application to communicate with your database, creating and droping tables, adding and removing fields, and specifying field types.

### Models
Models inherit from `ApplicationRecord` which in turn inherits from `ActiveRecord::Migrations`
As it is implemented in Rails, the models are the Ruby classes housed in `$YOUR_RAILS_APP_DIR/app/models`.
Models are the classes which contain the business logic of your application. Here you will write **Active Record Validations** which will be run on new instances of your objects.
Here you will also specify the connections and cardinality among your tables using **Active Record Associations**
Models classes, at their most basic form, serialize the data input into an instance of an object by the classes name.
They also reveal fundamental CRUD operations (Create, Read, Update, and Delete) to your rails application.


#### CRUD operations

##### Create (Klass.create, Object.save)
Thus, upon instantiating an instance of the model class `Dog`, `fido = Dog.new("fido")` an object is stored in memory.
However, if one were to exit the rails consoles after creating that instance, it would be garbage collected.
If one would like to persist this serialized object the database, one could type `fido.save`.
These operations of serializing the input data and then persiting to the database is the create operation and can be done by simply typing `Dog.create("fido")`.

##### Read (Klass.all, Klass.find(), etc.)
Since read operations inherently are leveraging the power of SQL queries, there are a plethora of differnt methods which one can use to read from ones database.
The full set of queries which have been implemented for supported databases are shown in the **Active Record Query Interface** docs.
One is also free to create ones own custom SQL queries; however, this has to be done with caution due to the risk of SQL injection attacks.

##### Update (e.g.: user = Klass.find_by(first_name: 'Elissa'); user.update(last_name: 'Khoury')
Just as in a SQL query we have to select a given record to update it, here too we have to use a read operation to first serialize the database record into a Ruby object which we can alter its data and then update the record in the database.
We can also update all records as well using the update_all method of the class which was inherited from ApplicationRecord: Klass.update_all "max_login_attempts = 3, must_change_password = 'true'".

##### Delete (program = Klass.find_by(name: 'sharepoint'); program.destroy)
Again, here we must first complete a query to reserilize the record into a Ruby object; then, we delete the record from the database.

#### Active Record Associations:
In Rails, we can leverage Active Record Associations to connect our models. This allows us to have one to one, one to many, many to many, and other relationships.
Please see the docs on AR Associations for full details.

### Controllers
Controllers provide up to seven basic RESTful model methods which determine what the HTTP verbs used to contact your applicaiton do.
In specific, they orchestrate the basic framework (which can be customized as you see fit) of receiving HTTP requests and translating those into calls on your models for queries and then specify which views should be presented.
Controllers also have the very important task of sanitizing such requests by using the private methods and params to control what fields are available.
Params is an absolute necessity to ensure security of your database so that malicious HTTP request cannot get what it requests.

## Generating Migrations, Models, Scaffolds, etc.
For full details, please refer to the **Active Record Migrations** docs.

The rails cli utility offers many time saving shortcuts which allow you to flesh out a 
a working application in a few in the terminal. Rails of course is a very opinionated
framework and it sets up several defaults which you may need to adjust to your needs.

The principle generators which you can employ are migration, model, and scaffold.
The order reflects the least to the most complex (and hence from fewer to more files created).
Rails scaffold generator in particular is very powerful if you need to quickly build out a full featured application.
However, if misused, it will actually just create a of bloat.

All generators are invoked through the cli with this syntax: `rails generate` and then the name of the generator.
A shortcut for this is `rails g` and then the generator you require.

This section will focus on the basics of this. One very useful flag which one can pass to `rail g` is the `-p` flag which will give you a preview of what the migration will do.
If you wish to delete all files associated with the migration, you can pass the `-d` flag at the end of the migration statement which refers to the migration you made.

### Migrations
Although they are not strictly migrations, it is important to know how to create databases and drop databases from Rails.
When first downloading this application, you should run `rake db:setup` this will reference `$YOUR_RAILS_APP_DIR/config/database.yml` and create the databases specified in that config file.
The opposite of this is completed by running `rake db:drop`.

Now, back to migrations. Again, to emphasize, migrations perform non-record level operations on your database. Hence, you can create or drop tables with them, create or drop columns/fields, but no record level opearations are performed (i.e., CRUD operations which are handled by Models).
They also serve as a somewhat basic version control system for defining and reverting non-record based changes. That said, when migrating a database to a new server, one should not use these migrations as this could be faulty. It is better to make a database dump to use on the new system.

#### `rails g migration Create___User___ name:string age:integer is_star_trek_fan:boolean`
Using `rails g migration CreateZZZ` followed by a set of key value pairs will invoke active_record and generate a new table ZZZ to be set up in your database with columns/fields for each key of the data type specified by the value.
```bash
Running via Spring preloader in process 8962
      invoke  active_record
      create    db/migrate/20190421040854_create_user.rb
```

Thus, only one file is generated, the one in `db/migrate`

To actually create the table in your database, you then need to run `rake db:migrate` which invokes the outstanding migrations.
If you decide that you did not want to do this, you can run `rake db:rollback` which will attempt to reverse the migrations just performed.

