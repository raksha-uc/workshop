# Django Templates
Being a web framework, Django needs a convenient way to generate HTML dynamically.
You see, in HTML, you can't really write Python code, because browsers don't understand it. They know only HTML. We know that HTML is rather static, while Python is much more dynamic.

Django template tags allow us to transfer Python-like things into HTML, so you can build dynamic websites faster.

1. ### Templates
   A template is a text file. It can generate any text-based format (HTML, XML, CSV, etc.).

   A template contains variables, which get replaced with values when the template is evaluated, and tags, which control the logic of the template.
   Example:
   ```
   {% extends "base_generic.html" %}

   {% block title %}{{ section.title }}{% endblock %}

   {% block content %}
   <h1>{{ section.title }}</h1>

   {% for story in story_list %}
   <h2>
   <a href="{{ story.get_absolute_url }}">
    {{ story.headline|upper }}
   </a>
   </h2>
   <p>{{ story.tease|truncatewords:"100" }}</p>
   {% endfor %}
   {% endblock %}

   ```
2. ### Variables
    A variable outputs a value from the context, which is a dict-like object mapping keys to values.
    Variables are surrounded by {{ and }} like this:

    To print a variable in Django templates, we use double curly brackets with the variable's name inside, like this:
   Example: 
   ```
   My first name is {{ first_name }}. My last name is {{ last_name }}.
   ```
   With a context of {'first_name': 'John', 'last_name': 'Doe'}, this template renders to:
   ```
   My first name is John. My last name is Doe.
    ```
3. ### Tags
    Tags provide arbitrary logic in the rendering process.

    Tags are surrounded by {% and %} like this:
    ```
   {% csrf_token %}
   ```

4. ### Filters
    Filters transform the values of variables and tag arguments.

    They look like this:
    ```
   {{ django|title }}
   ```
   With a context of {'django': 'the web framework for perfectionists with deadlines'}, this template renders to:
   ```
   The Web Framework For Perfectionists With Deadlines
   ```
   Some filters take an argument:
   ```
   {{ my_date|date:"Y-m-d" }}
   ```
   Django provides about sixty built-in template filters. You can read all about them in the built-in filter reference. To give you a taste of what’s available, here are some of the more commonly used template filters:

   - **default**:If a variable is false or empty, use given default. Otherwise, use the value of the variable. For example:
   ```
   {{ value|default:"nothing" }}
   ```
   If value isn’t provided or is empty, the above will display “nothing”.

   - **length**:Returns the length of the value. This works for both strings and lists. For example:
   ```
   {{ value|length }}
   ```
   If value is ['a', 'b', 'c', 'd'], the output will be 4.
5. ### Comments
    Comments look like this:
    ```
   {# this won't be rendered #}
   ```
    A {% comment %} tag provides multi-line comments.
6. ### Components
   - **Engine**: 
django.template.Engine encapsulates an instance of the Django template system. The main reason for instantiating an Engine directly is to use the Django template language outside of a Django project.
django.template.backends.django.DjangoTemplates is a thin wrapper adapting django.template.Engine to Django’s template backend API.

   - **Template**:
django.template.Template represents a compiled template. Templates are obtained with Engine.get_template() or Engine.from_string().
Likewise django.template.backends.django.Template is a thin wrapper adapting django.template.Template to the common template API.

   - **Context**:
django.template.Context holds some metadata in addition to the context data. It is passed to Template.render() for rendering a template.
django.template.RequestContext is a subclass of Context that stores the current HttpRequest and runs template context processors.
The common API doesn’t have an equivalent concept. Context data is passed in a plain dict and the current HttpRequest is passed separately if needed.

   - **Loaders**:
Template loaders are responsible for locating templates, loading them, and returning Template objects.

