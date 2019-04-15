# rails_university

rails_university is a generalized web application for university departments. This project will evolve into a generalized Rails API for the backend of such a web application which will allow the development of various UIs (desktop, mobile, etc.) to easily be built on top of it. Eventually, this project will be forked and it will also provide documentation on how to build a Docker image of it and run it as a container. 

The underlying database which has been chosen for this project is PostgreSQL due its being open-source and highly robust for high traffic volume. This `README` should provide basic information on how to get this application up and running so that one can focus on modifying it according to ones institution's needs.

## Dependencies 
The installation of PostgreSQL is highly dependent on the OS one chooses as is RVM. Once these dependencies are met, please skip to the set up section for detail on how correctly set up and configure PostgreSQL and RVM.

- [PostgreSQL 11](https://www.postgresql.org/download/ "PostgreSQL 11")
- [RVM](https://rvm.io/ "RVM")
- [Ruby 2.6.2](https://www.ruby-lang.org/en/ "Ruby 2.6.2")
- [Rails 5.2.3](https://github.com/rails/rails/tree/v5.2.3 "Rails 5.2.3")

## Set up
### Use RVM to install Ruby 2.6.2.

```bash
rvm install 2.6.2

# if you wish to use Ruby 2.6.2 by default, run:
rvm --default use 2.6.2
```

### Install necessary Ruby gems (including Rails)

```bash
# update your gems:
gem update --system

# if you want to save disk space, run:
echo "gem: --no-ri --no-rdoc" >> $HOME/.gemrc

gem install rails -v 5.2.3
```
