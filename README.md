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

### Creating Views:
16. In hello_world/views.py, below from django.shortcuts import render, type:

`from django.http import HttpResponse`

17. Below the # Create your views here. comment, create the following Python function named index. Inside the function, we are returning a simple HTTP response.

18. Within parentheses after HttpResponse add the string "Hello, world!"

### Creating our URLs:
19. In my_project/urls.py, You'll see that this urls.py file already has some content in it. That's fine, we will need that in future. Let's include the view we just created.

20. Import the `include `function by appending it after a comma to the existing `django.urls import`.

21. Below that, import the views from the hello_world app.

`from hello_world import views as index_views`

Here we are giving the hello_world/views.py file an alias of `index_views`. In a one-app project, this would not be strictly necessary. However, in a multiple-app project using descriptive alias names makes your urls.py file much easier to read and maintain.

22. Above the admin pattern in urlpatterns add:

`path('', index_views.index, name='index'),`

### settings.py:
23. Finally, we just need to add our app to the **settings.py** file to connect the app to the project. For our simple app, this is not strictly necessary, but it's good practice and will be required later on when app models are connecting to databases.

To connect the app you will need to scroll down through the my_project/settings.py file to find the `INSTALLED_APPS` list.

24. Append `'hello_world'`, to the end of the list of `INSTALLED_APPS`.

Note: Don't forget the comma at the end.

### Testing our app:
25. Always make sure to always save all your files before running the project. You can also take this opportunity to git add, commit and push your work.

26. Open a browser window by returning to the terminal tab and running the Django server with the same command as you did previously, and now you can see the text Hello, world! In the browser.
`python3 manage.py runserver`