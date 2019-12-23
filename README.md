# voila-simple-app

A simple web app build with Volia, a Python package to convert Jupyter notebooks into standalone web apps

## To replicate this deployment

### Create a new GitHub repo and connect the remote repo to the local folder

Create a new repo on GitHub.com, then link it to local folder

```text
mkdir voila-simple-app
cd voila-simple-app
git init
git remote add origin https://github.com/<UserName>/<RepoName>.git
git pull origin master
```

### Set up Python virtual env and install Jupyter and Voila

```text
python -m venv venv
source venv/bin/activate
pip install jupyter voila
```

### Create the Jupyter notebook that will be deployed with Voila

```text
jupyter notebook
```

In save the Jupyter notebook as ```app.ipynb```. Save the following code in the notebook

```text
# Voila App

import ipywidgets as widgets
from IPython.display import display

w = widgets.IntSlider()
display(w)
```

### Run Voila Locally

```text
voila app.ipynb
```

```[Ctrl-c]``` to exit

### Add three files required by Heroku

 * ```requirements.txt```
 * ```runtime.txt```
 * ```Procfile```

```text
pip freeze > requirements.txt
```

```text
nano runtime.txt
```

Inside ```runtime.txt```:

```text
python-3.7.6
```

```text
nano Procfile
```

Inside ```Procfile```:

```text
web: voila --port=$PORT --no-browser app.ipynb
```

### Add, commit and push changes up to GitHub

```text
git add .
git commit -m "initial commits for simple voila app to Heroku"
git push origin master
```

### Log into Heroku and push to Heroku

[Install the Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli) and [sign up for a Heroku Account](https://signup.heroku.com)

```text
heroku login
heroku create
git push heroku master
heroku open
```

### If there are problems, check the Heroku log

```text
heroku logs --tail
```
