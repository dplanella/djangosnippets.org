# Ubuntu snippets site

Experimental build of an Ubuntu snippets sharing site, based on the code
that powers djangosnippets.org

## Development setup

### Install system requirements

For testing purposes on a local machine, it's recommended to run the 
development server using virtualenv

    sudo apt-get install python-dev virtualenv ruby-compass

### Check out the code and set up the virtualenv

    $ git clone git@github.com:dplanella/ubuntusnippets.git
    $ cd ubuntusnippets
    $ virtualenv .
    $ source bin/activate

### Install app requirements and run
    
    $ cd requirements
    $ pip install -r development.txt
    $ cd ..
    $ python manage.py syncdb --migrate

Now you can start the develoment server::
    
    $ python manage.py runserver

Before you can actually use the site now you have to define at least one
language. If you just want to use the ones from djangosnippets.org, they
are included in the fixtures folder::
    
    $ python manage.py loaddata fixtures/languages.json

Now you should be able to use the development version of djangosnippets
pointing your browser to http://localhost:8000.


## Styling contributor?

DjangoSnippets uses the [Ubuntu Web Style Guide](http://design.ubuntu.com/web-style-guide)
as core of its visual style.

Any additional local styles are added using SASS syntax and compiled into the
final stylesheets using [compass](http://compass-style.org). Please modify
only the .scss source files in `ubuntusnippets/static/scss`, as the generated
.css files will be overwritten on each compass run.

To generate the CSS, simply run following commands in your terminal:
    
    $ cd ubuntusnippets/static
    $ compass watch

It is recommended that for the sake of production deployments you commit the 
compressed version of the CSS files. Here's an example, but 
[you can do this in different ways](http://compass-style.org/help/tutorials/production-css/):

    $ compass compile -e production --force

## Production setup

The recommended production setup uses gunicorn, nginx and elasticsearch.
