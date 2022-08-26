# Minimal template for a Django project configured with TailwindCSS and daisyUI ready to be deployed to Heroku

This code will set-up a Django Project with tailwindCSS and daisyUI ready to be deployed to Heroku.

This template was created alongside a this [blogpost](https://kenshuri-blog.herokuapp.com/posts/005_deploy_to_heroku.md)

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

## Deploy your project to Heroku

#### [Create a Heroku Remote](https://devcenter.heroku.com/articles/git#create-a-heroku-remote)

```shell
heroku create -a deploy-to-heroku-blog-example
git remote -v
```

#### [Deploy the code](https://devcenter.heroku.com/articles/git#deploy-your-code)

```shell
git push heroku main
```