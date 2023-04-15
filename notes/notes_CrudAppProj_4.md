# Chapter 3 Part 4: "Creating post_save Signal for Profile Creation"
## Notes setup
Video titles should be double quoted and in a `##` header

    ## Video "Thing"

Notes should follow with a `###` header along with new sections of code discussion. Like when editing a different file but within the same video / area.

    ### Moved to folder/file.ext inside of video "Thing"

Use the `>` block quote to reference which file is being edited.

    > My Example code: folder/file.ext

# A signal for new profiles!
A user and profile are currently not setup. I had to create a profile from the user.

## Django Singals
[Crash Course from same teacher](https://www.youtube.com/watch?v=W8MLlwvSS-U)

1. `touch profiles/signals.py`

> Create signal file: profiles/signals.py

``` python
# profiles/signals.py
from .models import Profile
from django.contrib.auth.models import User
from django.db.models.signals import post_save
from django.dispatch import receiver

@receiver(post_save, sender=User)
def post_save_create_profile(sender, instance, created, *args, **kwargs):
    print(sender)
    print(instance)
    print(created)
    if created:
        Profile.objects.create(user=instance)
```
### NOTES
`created` is a boolean which is passed along. Those *args and **kwargs are new to me... Lets take a look in the next section. Moving through this code we can see that we are importing the `Profile` class from the models and checking if `created` is `True` we create a new user. We see the `@` notation from FastAPI again. 

### *args and **kwargs wtf?
[From freeCodeCamp.org](https://www.freecodecamp.org/news/args-and-kwargs-in-python/)
It stands for many arguments and many keyword arguments it allows python to accept many arguments without writing a lot of different functions.

## Overide to register the signal
I will be honest this doesnt make a lot of sense but there is an entire hour long video that is a "crash course".

> Update with a ready: profiles/apps.py

``` python
# profiles/app.py
from django.apps import AppConfig


class ProfilesConfig(AppConfig):
    name = 'profiles'

    def ready(self):
        import profiles.signals
```

> Update the default: profiles/__init\__.py

``` python
# profiles/__init__.py
default_app_config = 'profiles.apps.ProfilesConfig'
```

### NOTES
This will setup a init.py that will call the ProfilesConfig class and setup the ready function which in turns waits for signals.py to be called. The ready command we setup in the ProfilesConfig is automatically called.

When an account is created it is set to True only once. Thats when the function is called and if it is true it creates a profile based on that user. This could also be where an email could be sent to the user to confirm the new account as well! In classic "program it your damn self" method.

