# Chapter 3 Part 3: "Creating the Models"
## Notes setup
Video titles should be double quoted and in a `##` header

    ## Video "Thing"

Notes should follow with a `###` header along with new sections of code discussion. Like when editing a different file but within the same video / area.

    ### Moved to folder/file.ext inside of video "Thing"

Use the `>` block quote to reference which file is being edited.

    > My Example code: folder/file.ext

## Creating the profiles model

> Updating: profiles/models.py

``` python
# profiles/models.py
from django.contrib.auth.models import User
# Create your models here.


class Profile(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE)
    bio - models.TextField(blank=True)
    avatar = models.ImageField(default='avatar.png', upload_to='avatars')
    updated = models.DateField(auto_now=True)
    create = models.DateField(auto_now_add=True)


    def __str__(self):
        return f"profile of the user {self.user.username}"
```

### NOTES
Lets break it down. We are importing a lovely premade class `User` to help fill out this class model. This looks alot like pydantic's model. 

### Adding avatar default file
> [avatar source](https://pixabay.com/vectors/user-avatar-log-in-photo-1808597/) added to media/avatar.png


## Creating the posts model

> Updating: posts/model.py

``` python
# posts/model.py
from django.db import models
from django.contrib.auth.models import User
from profiles.models import Profile
# Create your models here.

class Post(models.Model):
    title = models.CharField(max_length=300)
    body = models.TextField()
    liked = models.ManyToManyField(User, blank=True)
    author = models.ForeignKey(Profile(), on_delete=models.CASCADE)
    updated = models.DateField(auto_now=True)
    create = models.DateField(auto_now_add=True)


    def __str__(self):
        return str(self.title)
```

### NOTES
Not too much different from the profile model and we get to see the author variable added and linked to the Profile class. The interest one is the ManyToManyField that could be useful for the blog but its a feature that could be ignored.

## Its time for Migrations!
Lets setup the migrations with these new models!

1. `python manage.py makemigrations`
1. `python manage.py migrate`

Its like magic! :sparkles:  

## Add the new models into the admin panel

> Update: posts/admin.py
``` python
# posts/admin.py
from django.contrib import admin
from .models import Post
# Register your models here.

admin.site.register(Post)
```

> Update: profiles/admin.py
``` python
# profiles/admin.py
from django.contrib import admin
from .models import Profile

admin.site.register(Profile)
# Register your models here.

admin.site.register(Profile)```
```

### NOTES
Create a new user and change the profile picture and see the `media/avatars` directory get created automatically and new picture!

Should we look into possible attack vectors for files like this? Or maybe just disable new user creation? We do that for wordpress.

Created a new post without thinking about it. So far this has been very refreshing of the first Django app I tried to make up until the massive bugs that broke the front end yay!

I also added the gitignore file and it updates the color of the files in the file explorer which is really neato. I ensured that any new avatars dont accidently get sent to github - mostly a space saving measure - and the database since I am not sure what kind of PII might be stored here.

Adding some base notes in the main README.md