# Minimal template for a Django project configured with TailwindCSS and daisyUI ready to be deployed to Heroku

This code will set-up a Django Project with tailwindCSS and daisyUI ready to be deployed to Heroku.

This template was created alongside this [blogpost](https://kenshuri-blog.herokuapp.com/posts/005_deploy_to_heroku.md)

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

## Deploy your project to CapRover

#### Create a CapRover app

#### Deploy to CapRover

In the terminal run
```shell
caprover deploy
```

Follow the prompts and chose the app you just created

#### Modify your app environments variables

Add the following environment variables to your app:

* DJANGO_DEBUG=TRUE
* DJANGO_SECRET_KEY --> Create a secret key
* APP_ALLOWED_HOST --> Your app address