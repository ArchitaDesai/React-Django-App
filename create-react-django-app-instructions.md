# Instructions for creating django react web app from scratch


### Idea:
- Make repo for the initial setup, and once cloned you just need to run 1-2 commands and you're ready to go!


```
mkdir project

cd project

mkdir backend

npx create-react-app frontend

virtualenv env

source env/bin/activate

pip install django

pip install whitenoise
```

- note: requirements.txt will be same as mentioned
- So we can also do `pip install -r requirements.txt`
- `build.sh` will also remain same
- package.json will be same for npm watch
- Dont forget to mention npm-watch as dev dependency


```
cd backend

django-admin startproject projectname .



```

- Change structure of Django code - settings.py, views.py, urls.py

#### settings.py

- From `BASE_DIR`, replace with these lines

```
# Build paths inside the project like this: os.path.join(BASE_DIR, ...)
BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))

# rename backend for clarity
BACKEND_DIR = BASE_DIR

# from 'backend' directory, frontend's path = '../frontend'
FRONTEND_DIR = os.path.abspath(os.path.join(BACKEND_DIR, '..', 'frontend'))

# Add static files directory to serve JS and CSS for frontend react app
# Static files directory = 'frontend/build/static'
STATICFILES_DIRS = [os.path.join(FRONTEND_DIR, 'build', 'static')]
```

- Allowed hosts
```
ALLOWED_HOSTS = ['localhost', '127.0.0.1', '0.0.0.0']
```

- Add whitenoise inside INSTALLED_APPS, above django.contrib.staticfiles
```
# Whitenoise allows to take advantage of the staticfiles contrib app and its ecosystem.
# We can serve static files with WhiteNoise and cache them with CDN for performance.
'whitenoise.runserver_nostatic',	
```

- Add it inside MIDDLEWARE after 'django.middleware.security.SecurityMiddleware'

```
# Whitenoise middleware
# With a couple of lines of config WhiteNoise allows your web app to 
# serve its own static files, making it a self-contained unit that can be
# deployed anywhere without relying on nginx, Amazon S3 or any other external 
# service. (Especially useful on Heroku, OpenShift and other PaaS providers.)
'whitenoise.middleware.WhiteNoiseMiddleware',
```

- Add `os.path.join(FRONTEND_DIR, 'build')` inside `TEMPLATES.DIRS`

- In the end:

```
# STATICFILES_STORAGE = ('whitenoise.storage.CompressedManifestStaticFilesStorage')

STATIC_ROOT = os.path.join(BACKEND_DIR, 'static')


# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/2.2/howto/static-files/


STATIC_URL = '/static/'

# Serve static files with WhiteNoise and cache them
WHITENOISE_ROOT = os.path.join(FRONTEND_DIR, 'build', 'root')
```

#### Copy views.py and urls.py



### After going inside `frontend` directory 

```
cd frontend

# Don't forget to activate virtualenv before running npm watch or build script

source ../env/bin/activate

npm install
```

