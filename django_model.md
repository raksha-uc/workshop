# DJANGO MODELLING:
## What is Django Model?
A Django model is the built-in feature that Django uses to create tables, their fields, and various constraints.
In short, Django Models is the SQL of Database one uses with Django. SQL (Structured Query Language) is complex and involves a lot of different queries for creating, deleting, updating or any other stuff related to database. Django models simplify the tasks and organize tables into models. Generally, each model maps to a single database table. 
This article revolves about how one can use Django models to store data in the database conveniently. Moreover, we can use admin panel of Django to create, update, delete or retrieve fields of a model and various similar operations. Django models provide simplicity, consistency, version control and advanced metadata handling. 

Basics of a model include: 

- Each model is a Python class that subclasses django.db.models.Model.

- Each attribute of the model represents a database field.

## Making queries
We’ll refer to the following models,
   ```
   from django.db import models
   
   
   class Question(models.Model):
       question_text = models.CharField(max_length=200)
       pub_date = models.DateTimeField('date published')
       
       def __str__(self):
        return self.question_text
   
   
   class Choice(models.Model):
       question = models.ForeignKey(Question, on_delete=models.CASCADE)
       choice_text = models.CharField(max_length=200)
       votes = models.IntegerField(default=0)
       
       def __str__(self):
        return self.choice_text
   ```

1. ### Creating Objects:
   A model class represents a database table, and an instance of that class represents a particular record in the database table.
   To create an object, instantiate it using keyword arguments to the model class, then call save() to save it to the database.
   This performs an INSERT SQL statement behind the scenes. Django doesn’t hit the database until you explicitly call save().
The save() method has no return value.
   ```
    from app.models import Question
    b = Question(question_text='What is Model?', pub_date='1999-10-02')
    b.save()

   ```
   
2. ### Saving ForeignKey and ManyToManyField fields:
   
3. ### Retrieving all objects
   The simplest way to retrieve objects from a table is to get all of them. To do this, use the all() method on a Manager:
   ```
   all_entries = Question.objects.all()
   ```
   Refer: https://docs.djangoproject.com/en/4.0/topics/db/queries/#retrieving-specific-objects-with-filters

4. ### Retrieving a single object with get
   If you know there is only one object that matches your query, you can use the get() method on a Manager which returns the object directly
   ```
   one_entry = Question.objects.get(pk=1)
   ```
5. ### Field lookups
   Field lookups are how you specify the meat of an SQL WHERE clause. They’re specified as keyword arguments to the QuerySet methods filter(), exclude() and get().
   ```
   Question.objects.filter(pub_date__lte='2006-01-01')
   ```