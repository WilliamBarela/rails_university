# Rails Guide

## What is an Ruby on Rails?

Ruby on Rails is a *Model* *View* *Controller* (MVC) framework which is very powerful and values convention over configuration.
MVC is a common pattern for web applications and seeks to ensure separtation of concerns within the code base.
In addition to this, there are also several other features which make it easy for a developer to quickly build out a web application.
Rails can be very feature filled and allows for several other classes including a testing framework, mailers, and storage classes.

## What is an MVC? How does it connect to the database?

### Migrations
A web application without persistance in a database can only be classed as little more than a front-end.
As a result, one could write SQL to connect to the database and persist these values; however, that is brittle as it locks you into the SQL specification of one given database.
Thus, Rails also has migration classes which are stored in `$YOUR_RAILS_APP_DIR/db/migrations`.
Migrations are Ruby classes as well which inherit from the `ActiveRecord::Migration` class.
They are an *ORM* (objection relationship mapping) which allows for database independance (Rails is open source and many people have worked hard to include the SQL equivalent across several different RDBMS'.)
Migration classes specify which fields to add to which tables and what datatype they should be classed as.
Migrations also act as something of a version control system which you can use to communication from Rails to your database and go back to a previous moment in the databases development.
In sum, migrations allow your Rails application to communicate with your database, creating and droping tables, adding and removing fields, and specifying field types.

### Models
Models inherit from `ApplicationRecord` which in turn inherits from `ActiveRecord::Migrations`
As it is implemented in Rails, the models are the Ruby classes housed in `$YOUR_RAILS_APP_DIR/app/models`.
Models are the classes which contain the business logic of your application. Here you will write *Active Record Validations* which will be run on new instances of your objects.
Here you will also specify the connections and cardinality among your tables using *Active Record Associations*
Models classes, at their most basic form, serialize the data input into an instance of an object by the classes name.
They also reveal fundamental CRUD operations (Create, Read, Update, and Delete) to your rails application.


#### CRUD operations

##### Create (Klass.create, Object.save)
Thus, upon instantiating an instance of the model class `Dog`, `fido = Dog.new("fido")` an object is stored in memory.
However, if one were to exit bin/rails after creating that instance, it would be garbage collected.
If one would like to persist this serialized object the database, one could type `fido.save`.
These operations of serializing the input data and then persiting to the database is the create operation and can be done by simply typing `Dog.create("fido")`.

##### Read (Klass.all, Klass.find(), etc.)
Since read operations inherently are leveraging the power of SQL queries, there are a plethora of differnt methods which one can use to read from ones database.
The full set of queries which have been implemented for supported databases are shown in the *Active Record Query Interface* docs.
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

The rails cli utility offers many time saving shortcuts which allow you to flesh out a 
a working application in a few in the terminal. Rails of course is a very opinionated
framework and it sets up several defaults which you may need to adjust to your needs.

The principle generators which you can employ are migration, model, and scaffold.
The order reflects the least to the most complex (and hence from fewer to more files created).
All generators are invoked with this syntax: `rails generate` and then the name of the generator.
A shortcut for this is `rails g` and then the generator you require.

This section will focus on the basics of this.

### Migrations