# django-hello-world

## Create from scratch

```sh
# set up python dev environment
brew install pipenv
pipenv install django django-heroku gunicorn
pipenv shell

# wrap dependencies for Heroku
pip freeze > requirements.txt

# create Procfile for Heroku
echo 'web: gunicorn --pythonpath mysite mysite.wsgi' > Procfile # Heroku expects the project to be at root level. `--pythyonpath` allows it to be in a specified subdirectory path.

# add django_heroku settings
echo "import django_heroku
django_heroku.settings(locals())" >> mysite/mysite/settings.py

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

- [https://docs.djangoproject.com/en/2.1/intro/tutorial01/](https://docs.djangoproject.com/en/2.1/intro/tutorial01/)
- [https://devcenter.heroku.com/articles/django-app-configuration](https://devcenter.heroku.com/articles/django-app-configuration)

> Note: References preserved as PDFs in `docs/`.