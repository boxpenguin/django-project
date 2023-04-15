# Chapter 3 Part 1: "Creating Virtualenv and Setting Up the Django Project"
## Notes setup
Video titles should be double quoted and in a `##` header

    ## Video "Thing"

Notes should follow with a `###` header along with new sections of code discussion. Like when editing a different file but within the same video / area.

    ### Moved to folder/file.ext inside of video "Thing"

Use the `>` block quote to reference which file is being edited.

    > My Example code: folder/file.ext

## "Creating ~~virtualenv~~ pipenv..."
1. `git clone https://github.com/boxpenguin/django-project`
2. `cd ~/Development/django-project`
3. Run `~/Development/set-github` to set the git configs for this directory
4. `mkdir dj_ajax` to copy instructions
4. `sudo apt-get install cmake libtiff5-dev libjpeg8-dev libopenjp2-7-dev zlib1g-dev libfreetype6-dev liblcms2-dev libwebp-dev tcl8.6-dev tk8.6-dev python3-tk libharfbuzz-dev libfribidi-dev libxcb1-dev` Pillow headers and dependency
5. `pipenv shell`
6. `pipenv install django==3.1.7` Same as teacher
7. `pipenv install django-crispy-forms==1.11.1 pillow==8.1.0`
7. `codium .`

## "...Setting up the django project"
1. `cd dj_ajax`
2. `django-admin startproject posts_proj`
3. `mv posts_proj src`
4. `cd src`
5. `python manage.py migrate`
6. `python manage.py createsuperuser` Fill out with a super user
7. `python manage.py startapp posts`
8. `python manage.py startapp profiles`
9. `python manage.py runsever`
10. Click on link in terminal and go to /admin and login

### NOTES
Not much to say this is pretty much the same as the other projects I have done in Django. Even with an older version compared to the most recent version release.

This is a warmup for note taking really.

I should look into VSCode~~ium~~ videos to get better at using this editor.

Added a header gotcha with my desktop.

# Chapter 3 Part 2: Setting up the Django Project - Continuation
1. Skip to 13:00 - teacher covers a few hanging issues that I added to the previous section and how VSCode works.

> Adding django apps: posts_projs/settings.py
```python
# posts_projs/settings.py
# ...
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    # own apps
    'posts',    
    'profiles',
    # thirdparty
    'crispy_forms'
]
# ...
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [ BASE_DIR / 'templates'],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
# ...
STATIC_URL = '/static/'
STATICFILES_DIRS = [
    BASE_DIR / 'static'
    BASE_DIR / 'posts' / 'static',
    BASE_DIR / 'profile' / 'static',

]

MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'
```
### Add static directory/staic, template/static, and media directories
1. ` cd src`
1. `mkdir -p static/static templates/static media`

### Add a simple css file into static directory
1. `touch static/style.css`

> Adding some css: static/style.css
``` css
/* static/style.css */
.not-visible {
    display: none;
}
```
### Add a functions javascript file into static directory
1. `touch static/functions.js`

> Adding some css: static/functions.js

Left blank

### NOTES
This is also some simple django lessons at this point we are updating the settings.py to include our new "apps" `profile` and `posts`. We also include the static and template directory - which isnt created automatically.

Interestingly the teacher had us create a dummy-like css file thats blank? or `display: none` I have no idea what that is.

I added some linux commands to shorthand some simple Codium folder and file creations. I HAVE NO IDEA IF IT WILL WORK lol

> Updating: posts_proj/urls.py
``` python
from django.urls import path, include
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    path('admin/', admin.site.urls),
]

urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

### NOTES
Here we are doing some really good python code with the `+=` operator in appending to the `urlpatterns` list. Which according to this [post](https://www.codecademy.com/forum_questions/559a2e9576b8fec400000392) the `+=` operator acts like an `extend` and not `append` allowing multiple items to be added to a list. 

### Add some base html files to template/
1. `touch template/base.html template/navbar.html`

> Copy from github page template/base.html

[File hosted on github base.html](https://raw.githubusercontent.com/PacktPublishing/Django-with-JavaScript-and-Ajax/main/base.html)

### NOTES
`{% load static %}` is used to load the static files via insertion method `{% ... %}`. I dont know where "static" is being refered from but its not from posts_proj/setting.py. If its from the posts_proj urlpatterns its possible its running from there or that `static` is just a reserved word. Teacher says it just "loads static".

> template/navbar.html

Left blank

