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

```