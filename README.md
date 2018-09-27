# django-hello-world

## Create from scratch

### Requirements

- [git](https://git-scm.com)
- [homebrew](https://brew.sh)
- [python](https://www.python.org)
- [pip](https://pip.pypa.io/en/stable/)
- [pipenv](https://github.com/pypa/pipenv)
- [heroku cli](https://devcenter.heroku.com/articles/heroku-cli)

> Note: everything after homebrew should be installable via `brew install python pipenv heroku-cli`

```sh
# set up python dev environment
pipenv --three
pipenv install django django-heroku gunicorn
pipenv shell

# create the django project and app
django-admin startproject mysite
pushd mysite
python manage.py startapp myapp
popd

# create the Hello World! view
echo "from django.http import HttpResponse
def index(request):
    return HttpResponse('Hello, world!')" > mysite/myapp/views.py

# add the app route
echo "from django.urls import path
from . import views
urlpatterns = [
    path('', views.index, name='index'),
]" > mysite/myapp/urls.py

# add django_heroku settings
echo "import django_heroku
django_heroku.settings(locals())" >> mysite/mysite/settings.py

# update main project routes to direct towards app
sed -i '' 's/from django.urls import path/from django.urls import include, path/g' mysite/mysite/urls.py
sed -i '' 's/urlpatterns = \[/urlpatterns = \[\
    path(\'\', include(\'myapp.urls\')),/g' mysite/mysite/urls.py

# wrap dependencies for Heroku
pip freeze > requirements.txt

# create Procfile for Heroku
echo 'web: gunicorn --pythonpath mysite mysite.wsgi' > Procfile # Heroku expects the project to be at root level. `--pythyonpath` allows it to be in a specified subdirectory path.

# ignore the default sqlite database and python bytecode
echo "mysite/db.sqlite3
*.pyc" > .gitignore
```

## Deployment

### Local

```sh
pipenv shell
python mysite/manage.py runserver
open http://localhost:8000
```

### Locally with Heroku:

```sh
heroku local
open http://localhost:5000
```

## Deploying to Heroku

```sh
heroku create # make sure your ‘heroku’ git remote points to the correct app's git url, like if there was a previous one
git push heroku master
heroku open
```

## References

- [Writing your first Django app, part 1](https://docs.djangoproject.com/en/2.1/intro/tutorial01/)
- [Configuring Django Apps for Heroku](https://devcenter.heroku.com/articles/django-app-configuration)

> Note: References preserved as PDFs in `docs/`.