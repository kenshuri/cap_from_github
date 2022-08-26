# Minimal template for a Django project configured with TailwindCSS and daisyUI ready to be deployed to Heroku

This code will set-up a Django Project with tailwindCSS and daisyUI ready to be deployed to Heroku.

This template was created alongside a this [blogpost](https://kenshuri-blog.herokuapp.com/posts/005_deploy_to_heroku.md)

## Set-up the project

To set-up the project from scratch, run the following commands in your terminal.

```shell
git clone https://github.com/kenshuri/django_tailwind_heroku.git
cd django_tailwind_heroku
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
cd django_tailwind_heroku
cd jstoolchains
npm run tailwind-watch
```

In the second terminal run:
```shell
cd django_tailwind_heroku
python manage.py runserver
```

As prompted, open the page http://127.0.0.1:8000/ and enjoy 🚀

Note that changes in your html template `blogApp\templates\blogApp\index.html` automatically updates what you see in your browser.

## Deploy your project to Heroku

#### [Create a Heroku Remote](https://devcenter.heroku.com/articles/git#create-a-heroku-remote)

```shell
heroku create -a your-app-name-on-heroku
git remote -v
```

To make sure that your app can be accessed, you need to add your app domain on Heroku to the list of allowed host. 
Please change the setting in your `settings.py` file to match your app name on Heroku.

```python
# settings.py

ALLOWED_HOSTS = ['127.0.0.1', 'your-app-name-on-heroku.herokuapp.com']
```

Now commit the change:
```shell
git commit blogProject\settings.py -m 'Modify allowed hosts'
```

#### [Deploy the code](https://devcenter.heroku.com/articles/git#deploy-your-code)

```shell
git push heroku main
```

Finnaly, add the 2 following environment variable to your heroku app (by going in Settings > Config Vars):

- DJANGO_DEBUG = False
- DJANGO_SECRET_KEY = random value that you need to generate with code django function [`get_random_secret_key`](https://github.com/django/django/blob/3c447b108ac70757001171f7a4791f493880bf5b/django/core/management/utils.py#L82)