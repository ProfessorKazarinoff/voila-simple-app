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
pip install voila jupyter matplotlib numpy
```

### Create the Jupyter notebook that will be deployed with Voila

```text
jupyter notebook
```

In save the Jupyter notebook as ```app.ipynb```. Save the following code in the notebook

```text
import numpy as np
import matplotlib.pyplot as plt
from ipywidgets import interactive
%matplotlib inline

# Simple Voila App

## An easy way to deploy a Jupyter notebook to the cloud

def plot_func(a, f):
    plt.figure(2)
    x = np.linspace(0, 2*np.pi, num=1000)
    y = a*np.sin(1/f*x)
    plt.plot(x,y)
    plt.ylim(-1, 1)
    plt.title('a sin(f)')
    plt.show()

interactive_plot = interactive(plot_func, a=(-1.0, 1.0), f=(0.1, 1))
output = interactive_plot.children[-1]
output.layout.height = '300px'
interactive_plot
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
