# Heroku deployment

In this guide, we will be looking at how to deploy a Bocadillo application to Heroku.
You can find the example code in the [heroku-example](https://github.com/bocadilloproject/heroku-example) repo.

## Bocadillo application

Let's assume you have the following `app.py` script:

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

## Procfile

The [Procfile](https://devcenter.heroku.com/articles/procfile) is a text file located in the root directory of your project which explicitly declares what command should be executed to start your app.

As described in [Deployment](/discussions/deployment.md#running-with-gunicorn), the following should fit most use cases:

```
web: gunicorn -w 4 -k uvicorn.workers.UvicornWorker app:app
```

## requirements.txt

Heroku recognizes an app as a Python app by the existence of a Pipfile or requirements.txt file in the root directory. So mention all your python dependencies with the version in this file.

```
bocadillo
gunicorn
```

## runtime.txt

Place this file in the root directory with a specific Python version. [Heroku will look at it](https://devcenter.heroku.com/articles/python-runtimes) to determine which Python version to use.

```
python-3.6.8
```

## Heroku CLI

To interact with Heroku from the command line, make sure you have the [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli) installed.

## Create a Heroku application

```sh
heroku login    # This will ask you to enter email id and password

heroku create   # This will create an application in Heroku which you can see on Heroku Dashboard

git add .       # Add all the files

git commit -m “App ready to deploy”     # Commit the code

git push heroku master      # This will push the entire app on Heroku Server

heroku open     # Visit the app through generated URL or with this command

heroku logs     # This is to check the logs, if anything goes wrong.
```

That's it! You've just deployed a Bocadillo application to Heroku. 🚀
