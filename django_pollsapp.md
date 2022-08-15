# Creating Polls App
Open up your terminal where you want to create your project, and let’s first install django

    pip3 install django==3.1.14
This will install django in your system, and once it’s installed, we’re good to create a fresh project named SimplePoll. Run the following command in your terminal

    django-admin startproject SimplePoll
This will create a project named SimplePoll in your directory. 

create database pollsapp in postgres
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'pollsapp',
        'USER': os.environ.get('username', 'postgres'),
        'PASSWORD': os.environ.get('password', 'postgres'),
        'HOST': os.environ.get('host', 'localhost'),
        'PORT': os.environ.get('port', 5432),
    }
}
Migrate command is responsible for baking your database and creating tables and stuff.

    python3 manage.py migrate

    python3 manage.py makemigrations

Let’s create an application inside our project,get inside your project directory (SimplePoll), and from here, run the following command.

    python3 manage.py startapp PollApp

As the command says, it will just create an app inside the SimplePoll project directory. And now, go ahead and register your application into your project SimplePoll/settings.py.
```
    INSTALLED_APPS = [
        '...'
        'PollApp',
    ]
```
    
change in setting.py istalledapp
in models.py
    from django.db import models

    # Create your models here.
    
    
    class Choice(models.Model):
        name = models.CharField(max_length=20)
    
        def __str__(self):
            return self.name
    
    
    class Poll(models.Model):
        name = models.CharField(max_length=50)
        description = models.TextField()
        choices = models.ManyToManyField(
            Choice, related_name='related_polls', blank=True)
    
        def __str__(self):
            return self.name

python3 manage.py makemigrations

python3 manage.py migrate
python3 manage.py runserver

http://127.0.0.1:8000/admin
 python3 manage.py createsuperuser

