# simple-python-app

## Steps to build app to current state

```sh
$ brew install pipenv
$ pipenv install django django-heroku gunicorn
$ echo 'web: gunicorn --pythonpath mysite mysite.wsgi' > Procfile # Heroku expects the project to be at root level. `--pythyonpath` allows it to be in a specified subdirectory path.
$ pipenv shell
$ pip freeze > requirements.txt
```

Then follow the guides at [https://docs.djangoproject.com/en/2.1/intro/tutorial01/](https://docs.djangoproject.com/en/2.1/intro/tutorial01/) (PDF in `docs/`) to get a basic hello world app running locally, and [https://devcenter.heroku.com/articles/django-app-configuration](https://devcenter.heroku.com/articles/django-app-configuration) to get it running on Heroku.

> Note: instead of a simple “polls” app from the `djangoproject` guide, name it “myapp” for generics' sake.

In `mysite/settings.py`, add `import django_heroku` at top and `django_heroku.settings(locals())` at end.

## Deploying locally

```sh
$ cd mysite
$ pipenv shell
$ python manage.py runserver
$ open http://localhost:8000
```

Using `heroku local`:

```sh
$ cd mysite
$ heroku local
$ open http://localhost:5000
```

## Deploying to Heroku

```sh
$ heroku create
$ git push heroku master
$ heroku open
```