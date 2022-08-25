# Minimal template to set-up a Django project with TailwindCSS and daisyUI

As described, this code will set-up a Django Project with tailwindCSS and daisyUI. The auto-reload feature is also included.

The code for this was vastly inspired from a stackoverflow answer on [How to use TailwindCSS with Django?](https://stackoverflow.com/questions/63392426/how-to-use-tailwindcss-with-django#63392427).

## Set-up the project

To set-up the project from scratch, run the following commands in your terminal.

```shell
git clone https://github.com/kenshuri/setup_django_tailwind_daisyui.git
cd setup_django_tailwind_daisyui
python -m virtualenv venv
pip install -r requirements.txt
cd jstoolchains
npm install
```

You're good to go my friend!

## Start your project 

To see your project in action, open 2 terminals.

In the first terminal run:
```shell
cd setup_django_tailwind_daisyui
cd jstoolchains
npm run tailwind-watch
```

In the second terminal run:
```
cd setup_django_tailwind_daisyui
python manage.py runserver
```

As prompted, open the page http://127.0.0.1:8000/ and enjoy 🚀

Note that changes in your html template `blogApp\templates\blogApp\index.html` automatically updates what you see in your browser.

### Deploy to Heroku

#### [Create a Heroku Remote](https://devcenter.heroku.com/articles/git#create-a-heroku-remote)

```shell
heroku create -a deploy-to-heroku-blog-example
git remote -v
```

#### [Deploy the code](https://devcenter.heroku.com/articles/git#deploy-your-code)

```shell
git push heroku main
```

But it won't be so easy! You should see the below error message:
```
remote:  !     Error while running '$ python manage.py collectstatic --noinput'.
remote:        See traceback above for details.
remote:
remote:        You may need to update application code to resolve this error.
remote:        Or, you can disable collectstatic for this application:
remote:
remote:           $ heroku config:set DISABLE_COLLECTSTATIC=1
remote:
remote:        https://devcenter.heroku.com/articles/django-assets
remote:  !     Push rejected, failed to compile Python app.
remote: 
remote:  !     Push failed
remote: Verifying deploy...
remote:
remote: !       Push rejected to deploy-to-heroku-blog-example.
remote:
To https://git.heroku.com/deploy-to-heroku-blog-example.git
 ! [remote rejected] main -> main (pre-receive hook declined)
error: failed to push some refs to 'https://git.heroku.com/deploy-to-heroku-blog-example.git'
```

It's very normal as Django does not support serving static files in production. A solution is proposed below:

#### [Django and static assets in production](https://devcenter.heroku.com/articles/django-assets)

Follow instructions available on that [page](https://whitenoise.evans.io/en/stable/django.html). To sum-up, you'll need to:

- Install whitenoise
```shell
pip install whitenoise
```

- Add the following to your `settings.py`
```python
# settings.py

STATIC_ROOT = BASE_DIR / "staticfiles"
```

- Edit your `settings.py` file and add WhiteNoise to the MIDDLEWARE list. The WhiteNoise middleware should be placed directly after the Django SecurityMiddleware (if you are using it) and before all other middleware:
```python
# settings.py

MIDDLEWARE = [
    # ...
    'django.middleware.security.SecurityMiddleware',
    'whitenoise.middleware.WhiteNoiseMiddleware',
    # ...
]
```

Now, you could commit and try again to deploy your app to heroku...

```shell
git push heroku main
```

The deployment is successful!! Now go and check your app... What the heck ??!! Something is wrong and you should see an error message saying:
>#### Application error
>
>An error occurred in the application and your page could not be served. If you are the application owner, check your logs for details. You can do this from the Heroku CLI with the command
>
>`heroku logs --tail`

Again, this was to be expected, we're not done yet! At the moment, as indicated by the error message, there is **no web process running**.

#### Add a `Procfile` and setup `gunicorn`

As described [here](https://devcenter.heroku.com/articles/django-app-configuration), Heroku web applications require a `Procfile`. This file is used to explicitly declare your application’s process types and entry points. It is located in the root of your repository.

The `Procfile` uses `gunicorn`, we thus need to install it following the instructions available on [this page](https://devcenter.heroku.com/articles/django-app-configuration). As a summary:

- Install gunicorn
```shell
pip install gunicorn
```

- Add a `Procfile` to project root containing simply the following. The name of the app (before `.wsgi below`) is from the value of the `WSGI_APPLICATION` variable define in your `settings.py`.
```text
Procfile

web: gunicorn blogProject.wsgi
```

- Update your requirements.txt to add `gunicorn`
```shell
pip freeze > requirements.txt
```

- Commit and push to heroku


We're not there yet ! You should see an error message complaining about **DisallowedHost at /** 

#### Add ALLOWED_HOSTS

You need to specify in your `settings.py` that your application should accept connection coming from your application domain... To do so, modify the variable ALLOWED_HOSTS defined in your `settings.py`. In my case, in need to do:

```python
# settings.py

ALLOWED_HOSTS = ['deploy-to-heroku-blog-example.herokuapp.com']
```

Commit again, and push to heroku!

> Bravoooooo !!!!

You should see the landing page :) But wait, something is not right... 

...

...

...

The design is wrong !! Tailwind and daisyUI are not used !!!! This is the worst tutorial ever :'( 

Don't stop here my friend, the time has come: let's make it work with **tailwind + daisyUI**!



