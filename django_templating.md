# Django Templates
Being a web framework, Django needs a convenient way to generate HTML dynamically.
You see, in HTML, you can't really write Python code, because browsers don't understand it. They know only HTML. We know that HTML is rather static, while Python is much more dynamic.

Django template tags allow us to transfer Python-like things into HTML, so you can build dynamic websites faster.

1. ### Variables
    A variable outputs a value from the context, which is a dict-like object mapping keys to values.
    Variables are surrounded by {{ and }} like this:

    To print a variable in Django templates, we use double curly brackets with the variable's name inside, like this:

    ```
   {{ posts }}
   ```
2. ### Tags
    Tags provide arbitrary logic in the rendering process.

    Tags are surrounded by {% and %} like this:
    ```
   {% csrf_token %}
   ```

3. ### Filters
    Filters transform the values of variables and tag arguments.

    They look like this:
    ```
   {{ django|title }}
   ```
4. ### Comments
    Comments look like this:
    ```
   {# this won't be rendered #}
   ```
    A {% comment %} tag provides multi-line comments.