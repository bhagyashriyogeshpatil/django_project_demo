# Developing with Django

## Steps needed to create a simple app in Django:

### Create your repo:
1. Give your repo a unique descriptive name that is based on the project. I have used django-project-demo.
2. Click on Create repository from template.
3. Open in your preferred IDE.
4. In the main menu, click on Terminal > New Terminal.

### Installing packages:
5. Type the following command in the terminal to install the Django Python package:

`pip3 install Django~=4.2.1`

Note: ~=4.2.1 installs any package version greater than or equal to 4.2.1 but less than 4.3

6. Once the package is installed, add it to the requirements.txt file with the following command:

`pip3 freeze --local > requirements.txt`

7. It's good practice to check what packages have been installed. When you look in the requirements file, you can see that three packages were installed.

### Creating a Django project:
8. Return to the terminal. In the terminal, create a Django project called my_project in the current directory.

Important: Remember that the shortcut to refer to the current directory is a single dot . at the end of the command.

`django-admin startproject my_project .`

Note: Check in the explorer tab to see that the my_project project structure has been created.

<span style="color:#6495ED"><strong>Creating a project:</strong></span>

The django-admin startproject command expects to see a project name followed by a directory name. 

For example:

`django-admin startproject project_name directory_name`

The top level in Django is a project. A project is like a container for everything we want to do. By default, the project contains a settings file and some other administrative files.

Important files in our project folder:

- **settings.py**: this file contains the project-wide settings, such as installed apps and database connection information, among other things.

- **manage.py**: this file is in the root directory, above the project folder. It is used to create apps, run our project and perform some database operations.


9. Return to the terminal and start the Django server with the following command:

`python3 manage.py runserver`

10. Click on Open Browser.

11. This opens a scary-looking yellow error screen, don't worry! Your server is running properly. This error is telling you that, for security reasons, Django doesn't recognise the hostname - the server name your project is running on.

12. Select and copy the hostname after "Invalid HTTP_HOST header:". In this example, that is '8000-nielmc-django-project-0kylrta3cs.us2.codeanyapp.com' - you can include the quotes.

13. In the my_project/settings.py file, paste the hostname between the square brackets of ALLOWED_HOSTS and save. For the above example, this would look like:

`ALLOWED_HOSTS = ['8000-nielmc-django-project-0kylrta3cs.us2.codeanyapp.com']`

14. Now if you return to the browser tab and refresh you will see a bare-bones Django project.

Note: Return to the terminal and use ctrl-c to kill the server.

### Creating a Django app:
15. Now we have a Django project created, we need to make an app. To do this, we use the manage.py file. In the terminal, type:

`python3 manage.py startapp hello_world`

Note: Check the explorer panel to see the new hello_world app directory has been created.

<span style="color:#6495ED"><strong>Creating a project:</strong></span>

Inside the project, we create apps.
Simply put, apps are the building blocks of Django.

Important files in our apps folder:

- **models.py**: our database models are stored here, which define the structure of the database used by our app.

- **views.py**: this file contains the view code for our app. You’ve already created some view code to display a text response to the user.

### Creating Views:
16. In hello_world/views.py, below from django.shortcuts import render, type:

`from django.http import HttpResponse`

17. Below the # Create your views here. comment, create the following Python function named index. Inside the function, we are returning a simple HTTP response.

18. Within parentheses after HttpResponse add the string "Hello, world!"

        `# Create your views here.
         def index(request):
            return HttpResponse("Hello, world!")`



<span style="color:#6495ED"><strong>The request & response objects:</strong></span>

    `# Create your views here.
    def index(request):
        if request.method == "GET":
            return HttpResponse("This was a GET request")
        elif request.method == "POST":
            return HttpResponse("This was a POST request")`

The first argument passed into a view function represents the **HTTP request object**. By default, we call this parameter request, but you could call it anything you like.

The request object is one of the ways that Django transfers the **state** throughout the system. In programming, **state** is a program or application’s temporary data at a given moment in time.

A view receives data from the browser through the request object and returns it through a response object.

<span style="color:#6495ED"><strong>The request object:</strong></span>

The HTTP request object contains **metadata** about the request made to the browser. This includes the request method, as noted above. It also includes any form data, the URL that was called, and any files that were uploaded, among other things.

The view can then use the information in the request object to complete a task, such as writing form data to the database.

For a full list of the contents of the request object, you can check the [Django documentation](https://docs.djangoproject.com/en/4.2/ref/request-response/).


<span style="color:#6495ED"><strong>The response object:</strong></span>

Finally, each view must return a response object to the browser. In our simple example, we have returned a simple HttpResponse.

### Creating our URLs:
19. In my_project/urls.py, You'll see that this urls.py file already has some content in it. That's fine, we will need that in future. Let's include the view we just created.

20. Import the `include `function by appending it after a comma to the existing `django.urls import`.

21. Below that, import the views from the hello_world app.

`from hello_world import views as index_views`

Here we are giving the hello_world/views.py file an alias of `index_views`. In a one-app project, this would not be strictly necessary. However, in a multiple-app project using descriptive alias names makes your urls.py file much easier to read and maintain.

22. Above the admin pattern in urlpatterns add:

`path('', index_views.index, name='index'),`

<span style="color:#6495ED"><strong>Investigating URLs:</strong></span>

The steps in the Django request cycle:
- The user enters a URL to your site in their browser.
- Django’s URL router checks to see if the URL matches any known URLs.
- If the entered URL does not match anything in the urls.py files, then Django returns an error.
- If it does match, then Django passes control to the view specified in the URL. In our case, the view is called index.
- The view returns either a HttpResponse or a template. In our case, it returns a HttpResponse.

<span style="color:#6495ED"><strong>Importing views:</strong></span>

The first thing we need to do in our urls.py file is to import the views. We can then refer to these views in `urlpatterns`.

As you can see, close to the top of urls.py, we import the views from hello_world using this line:

`from hello_world import views as index_views`

When we import something in Python we can use the as keyword, this creates an alias, which is how we will refer to the import from now on. In this case, we will refer to the views we imported as index_views.

<span style="color:#6495ED"><strong>Importing views:</strong></span>

Then, the path function takes three arguments:

`path('hello/', index_views.index, name='index'),`

First is the URL pattern.

Then, the view to call. In our case, the index function from the views file we imported and aliased as index_views.

Finally, we have a friendly name for the view.

**IMPORTANT NOTE:** As shown above, you must add the trailing / to your URL patterns, otherwise they will not work.


### settings.py:
23. Finally, we just need to add our app to the **settings.py** file to connect the app to the project. For our simple app, this is not strictly necessary, but it's good practice and will be required later on when app models are connecting to databases.

To connect the app you will need to scroll down through the my_project/settings.py file to find the `INSTALLED_APPS` list.

24. Append `'hello_world'`, to the end of the list of `INSTALLED_APPS`.

Note: Don't forget the comma at the end.

### Testing our app:
25. Always make sure to always save all your files before running the project. You can also take this opportunity to git add, commit and push your work.

26. Open a browser window by returning to the terminal tab and running the Django server with the same command as you did previously, and now you can see the text Hello, world! In the browser.
`python3 manage.py runserver`