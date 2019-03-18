# Introduction

In this guide, we will be looking at how to deploy bocadillo powered app to Heroku.
You can see example code in [heroku-example](https://github.com/bocadilloproject/heroku-example) repo.

### Bocadillo Application

Assuming, you have `app.py` already installed and it may look similar to this:

```
from bocadillo import App

app = App()

@app.route("/")
async def index(req, res):
    res.text = "Hello, from Heroku!"


if __name__ == "__main__":
    app.run()
```

Make sure it is running in local machine.

```
python app.py
# Started server process
# Waiting for application startup.
# Uvicorn running on http://127.0.0.1:8000 (Press CTRL+C to quit)
```

### Procfile

A text file in the root directory of your application, to explicitly declare what command should be executed to start your app.

```
web: gunicorn -w 4 -k uvicorn.workers.UvicornWorker app:app
```

### Requirements.txt

Heroku recognizes an app as a Python app by the existence of a Pipfile or requirements.txt file in the root directory. So mention all your python dependencies with the version in this file.

```
bocadillo
gunicorn
```

### Runtime.txt

Have this file in the root directory with a specific python version. Heroku will look at it to determine which python version to use.

```
python-3.6.8
```

### Heroku CLI

To interact with Heroku from command line interface, install Heroku CLI or Toolbelt.

### Create a Heroku app & Deploy

```sh
heroku login    # This will ask you to enter email id and password

heroku create   # This will create an application in Heroku which you can see on Heroku Dashboard

git add .       # Add all the files

git commit -m “App ready to deploy”     # Commit the code

git push heroku master      # This will push the entire app on Heroku Server

heroku open     # Visit the app through generated URL or with this command

heroku logs     # This is to check the logs, if anything goes wrong.
```

And, Everything’s done !!
