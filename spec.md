# Specifications for Rails University MVP

Specs:
- [x] Include spec.md
- [ ] Use Ruby on Rails backend and frontend
- [ ] Use Entity Relationship Diagram as a guideline to design the following models
- [ ] Has >=1 `has_many` and `belongs_to` relationship(s)
- [ ] Has >=2 `has_many :through` relationships
- [ ] Has =1 many-to-many relationship(s) implemented with `has_many :through` relationship
- [ ] Join table for many-to-many relationship has >= 1 field other than FK which can be submitted by user UI
- [ ] Models defend against invalid data by the inclusion of validations
- [ ] Include >=1 class level ActiveRecord scope method [(AR scope reference)](https://guides.rubyonrails.org/active_record_querying.html#scopes "AR scope ref")
- [ ] Scope method is chainable (i.e., uses ActiveRecord Query method such as `.where`, `.order`, etc.)
- [ ] Provide standard user authentication (signup, login, logout, passwords)
- [ ] Provide >=1 Oauth login option through Github, Google, Facebook, Twitter, etc.
- [ ] Include and use nested resources and appropriate RESTful URLs for routing
- [ ] Include nested `new` route and related form to parent resource
- [ ] Include nested `index` or `show` route.
- [ ] Forms correctly display validation errors
- [ ] a. fields enclosed in `fields_with_errors` class
- [ ] b. error messages describing validation failures must be shown in view
- [ ] Application is DRY
- [ ] a. logic in controllers encapsulated as methods in models
- [ ] b. views use helper methods and partials when appropriate
- [ ] c. follow patterns in Rails and Ruby style guides (linked below)
- [ ] *DO NOT* use scaffolding generators

Confirm:
- [ ] You have a large number of small Git commits
- [ ] Your commit messages are meaningful
- [ ] You made the changes in a commit that relate to the commit message
- [ ] You don't include changes in a commit that aren't related to the commit message

Design Goals:
- [ ] SOLID
- [ ] GRASP

Instructions:
- [ ] Commit early and often (2..15 lines of code per commit); commit messages are meaningful and accurate
- [ ] >=30 min coding session record
- [ ] Checkmark spec.md and comment how specs were fulfilled
- [ ] Screencast explanation of app usage
- [ ] Blog project and process
- [ ] README.md includes a short description, install instructions, a contributors guide and a link to the license for your code

Reference and Follow:
- [ ] [Ruby Style Guide](https://github.com/rubocop-hq/ruby-style-guide "Ruby Style Guide")
- [ ] [Rails Style Guide](https://github.com/rubocop-hq/rails-style-guide "Rails Style Guide")
