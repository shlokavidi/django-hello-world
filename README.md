# django-hello-world

## Create from scratch

```sh
brew install pipenv
pipenv install django django-heroku gunicorn
echo 'web: gunicorn --pythonpath mysite mysite.wsgi' > Procfile # Heroku expects the project to be at root level. `--pythyonpath` allows it to be in a specified subdirectory path.
pipenv shell
pip freeze > requirements.txt
```

In `mysite/settings.py`, add `import django_heroku` at top and `django_heroku.settings(locals())` at end.

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

- [https://docs.djangoproject.com/en/2.1/intro/tutorial01/](https://docs.djangoproject.com/en/2.1/intro/tutorial01/)
- [https://devcenter.heroku.com/articles/django-app-configuration](https://devcenter.heroku.com/articles/django-app-configuration)

> Note: References preserved as PDFs in `docs/`.