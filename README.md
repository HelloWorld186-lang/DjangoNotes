# Django

## Start project

- Code for the starting the project in the django is :- ```django-admin startproject nameofproject```

- There is ```manage.py``` with the help of the this we get intract with the our django project

- There is folder which contain to many file .  They are :- 1. setting.py (in this we write all the setting of the django)2. url.py (in this we write all the url of the project)3.init.py (in this we write all the import from the project)4.wsgi.py(this is use to run the project(inside it all the code for the runing the project is gone to be written))

## How to make a app in the djnao 
- Write the code for making app in the djnao project. The code is ```python manage.py startapp nameofapp```
- The app is the folder which contain to many files . They are :- 1. init.py(same as the init.py for the whole project, but this is for the this app)2.admin.py (this is for the admin panel change)3.app.py(this is app file for this whole app)4.view.py(in this we gone to write all the logic for the project)6.model.py(in this we write all the data base for our project)7.test.py(in this we write all the testing code in it)
- It is to be noted that the djanog app are reusable and each app it own work in the project  for example auth app will handel all the work related to the authactication
- It is important to add each app in the installed app in the setting.py so the project can know that the app is for that project  

## Run the app on the local server
- Write the code for the doing it . The code for doing so is ```python manage.py runserver```
- If we want to run project on the diffrent socket . Then write code ```python manage.py runsever 0.0.0.0:5000```


## First response useing django is :- 
- code for the first repsonse is :- 
- In the home.view write the function and import hhtpsrepsonse 
- code is :- 
```
from djnago.hhtps import hhtpsrepsonse
def home(request):
    return httpsrepsonse('Hello world')
```
- and in the url of the djanog write the code 
- code is 
```from home.views import home```
and in the url function write the code :- 
```
path('' , home , name = "home') #this is for back ref to the home
```

### We never written simple text , we return the complex html code 

## First html code repsonse code 
- The code the url is same 
- make a directory of name templetes in the home then make index.html 
- In the view write the code-
```
def home(reuqest):
    return render(request , 'index.html')
```

## Template engine for the projecting the backend data into the frontend html code 
- Code for it is :-
- View.py code is :- 
```
def home(request):
    data = ['ayuh' , 'aryan' , 'many more']
    return render(request , 'index.html' , context={'data' : data})
```
- Index.html code :- 
```
{% for man in data%}
    <p><span>{{forloop.counter}}</span>{{man}}</p>
{% endfor %}
```
This text known as jinja text - in this {% write all the python logic in it%} and in this {{write the value need to show}}

## Dry (donot repate youself) according to this many code is gone to repeate so do this 
- Make a base html so write the common code in it and for using this use this thing 
- Base html codr is :- 
```
    {% block name_of_block %}
    {% endblock %}
```
- code for the other of them are 
```
{% extends 'base.html' %}
{% block name_of_block %}
 // simple code
{% endblock %}
```

## Add the model in the djnaog project
- code for it is :- 
```
class Nameofclass(models.Model):
    id = models.autofield()  this filed is gone to fill by the django and this is promary key (unique)
    name = models.CharField() 
    age = models.IntegerField()
    email = models.EmailField()
    image = models.ImageField()
    file = models.FileField()
```
- After any chnage in the model or make any 
model write the code :- 
```
python manage.py makemigrations
```
- After doing so we get migration folder which contain files in it , which noted that change in the model.py 
- ``` python manage.py migrate``` by this code , we can migrate the model in the sql lite 


## Shell in the djanog :- 
- Using the terminal we can iteract to the django directly code for it is :- 
```
python manage.py shell
```
- Bying doing so we can interact  with the data base 
- So we can do the crud operation in it (create , remove , update , delete)
- For example :- 
code for saving the data using shell 
- code for the model.py :- 
```
class User(models.Model):
    name = models.CharField()
  ```  
- code for the shell :- 
```
from home.models import User
user = User(name = "Ayush")
user.save()
```
- Very Important work of the shell is that we cannout directly run the function in the django , so we use the shell for doing this

#### In the django for the models we have the ```model manager ```the code 
- Example code with the shell if we want to save the user same as the we write this code
```
User.object.create(name = 'Ayush')
```
- And If i want to see all of them , then write the code 
```
User.objects.create(name = 'ayush') // this will return in the form of the array
```
- Above is in the form of the array , so we can get the specific name using the model manager 
```
User.objects.all()[0].name
```

## Now we are ready for the CRUD methode 
- Create methode :- 
- - code for creating data in the model is (usin g the model manger in the shell)
```
User.objects.create(name : 'Ayush')
```
- Reading methode :- 
- - code for reading data in the model is (using the model manger in the shell)
```
user = User.objects.all()
```
only chnage in the model class is :- 
```
def __str__(self):
        return self.name
```
This change because to print the name in the shell 
```
user = User.objects.all()
 for u in user:
     print(u.name)
```
This is the iterable methode.
```
filter
```
We can use the filter for the filtering the data according to the componet of the model. Example code is :- 
```
ayush = User.objects.all().filter(name = 'Ayush)
```
- Update Methode :- 
- - Using model manager we can also update the data . The code is 
```
 User.objects.all().filter(name = 'Ayush').update(name = 'Aryan')
```
- Delete methode :- 
- - This is the code for the deleting the data from the database
```
 User.objects.all().filter(name = 'Aryan').delete()
 ```

## Now we are going to make a django project :- Food recipe app 
- I make a form for the app :- 
- I use the django form 
- ## Django form:- 
- - Code is :- 
```
 <form method="post" enctype="multipart/form-data" class="h-auto w-full max-w-md p-8 bg-white rounded-lg shadow-lg">
        {% csrf_token %}
        <h2 class="text-2xl font-bold mb-6 text-red-500 text-center">Make Recipe Post</h2>
        <div class="mb-4">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="name">
                Recipe Name
            </label>
            <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="name" type="text" name="name" placeholder="Enter recipe name">
        </div>
        <div class="mb-4">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="desc">
                Description
            </label>
            <textarea class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="desc" name="desc" rows="3" placeholder="Enter recipe description"></textarea>
        </div>
        <div class="mb-6">
            <label class="block text-gray-700 text-sm font-bold mb-2" for="image">
                Image
            </label>
            <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="image" type="file" name="image">
        </div>
        <div class="flex items-center justify-center">
            <button class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" type="submit">
                Submit Recipe
            </button>
        </div>
    </form>
```
- The import part of the form is :- 
-  1. encrpt (use the multiple for the image or the file to include)
-  2. methode (use the post methode for making a post)
- 3. csrf_token (this ensure that the post make from the same server or not (to reduce unuse request))
- The views.py code is :- 
```
from .models import Recipe

def recipe_form(request):
    if request.method == 'POST':
        data = request.POST
        name = data.get('name')
        desc = data.get('desc')
        image = request.FILES.get('image')
        Recipe.objects.create(name=name, desc=desc, image=image)
        return redirect('/')
    return render(request, 'index.html')
```
- Important thing to see is that the image request requires extra that is ```FILES```
- ## Static media in the django 
- - To show the image in the django template from the django folder then we use this code :- 
```
import os
from pathlib import Path

# Build paths inside the project like this: BASE_DIR / 'subdir'.
BASE_DIR = Path(__file__).resolve().parent.parent

# Static files (CSS, JavaScript, Images)
STATIC_URL = '/static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')

# Additional locations of static files
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'static'),
]

# Media files (Uploaded files)
MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')

# Add this to your INSTALLED_APPS
INSTALLED_APPS = [
    # ... other apps ...
    'django.contrib.staticfiles',
]

# At the end of your settings.py file, add:
if DEBUG:
    STATICFILES_DIRS = [os.path.join(BASE_DIR, 'static')]
else:
    STATIC_ROOT = os.path.join(BASE_DIR, 'static')
```
```
from django.conf import settings
from django.conf.urls.static import static
from django.contrib import admin
from django.urls import path
from Home.views import recipe_form

urlpatterns = [
    path('', recipe_form, name='recipe_form'),
    path('admin/', admin.site.urls),
]

if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```
```
your_project/
    ├── static/
    └── media/
```
- Important to note that we have to write this code to load all the static folder files 
code in the top of the base html code the code is :- 
```{% load static %}```
- After doing so the file structue for the project is :- 
```    
my_project/
│
├── manage.py
├── my_project/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
│
├── my_app/
│   ├── migrations/
│   ├── static/
│   │   ├── css/
│   │   ├── js/
│   │   └── images/
│   ├── templates/
│   │   └── my_app/
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── tests.py
│   └── views.py
│
├── static/ # this is the that once about which we setup in the setting 
│   ├── css/
│   ├── js/
│   └── images/
│
├── media/# this is the that once about which we setup in the setting 
│
└── templates/
    ├── base.html
    └── other_global_templates.html
```
- Now how to excess the whole js and css of the static folder the code is 
```
<link href="{% static 'css/styles.css' %}" rel="stylesheet">
    <script src="{% static 'js/script.js' %}"></script>
```
- And for the image write the code in the url :- 
```
{% if recipe.image %}
    <img src="{{ recipe.image.url }}" alt="{{ recipe.name }}">
{% endif %}
```
Another methode is that :- 
```
in the url of the google :- media/foldernameofrecipe/imagename.png
```

- ## Django dynamic url making 
- - The url code for it is : - ```path('update/<int:id>', recipe_update, name='recipe_update')```
- - The view code for it is : - ```def recipe_update(request, id):``` get the id by name id 
- - And the anchore code is :- ```<a href="update/{{recipe.id}}">update</a>```

- ## Django search and __icontains
- - Code for the form of the search is :- 
```
<form class="w-full flex justify-center items-center h-12 border-2 border-gray-100 px-3 rounded-full overflow-hidden">
                            <input type="text" name="search" class="w-full focus:outline-none" placeholder="Search recipes...">
                            <button type="submit" class="flex-shrink-0 ml-2">
                                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="24" height="24" color="#F44336" fill="none">
                                    <path d="M17.5 17.5L22 22" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" />
                                    <path d="M20 11C20 6.02944 15.9706 2 11 2C6.02944 2 2 6.02944 2 11C2 15.9706 6.02944 20 11 20C15.9706 20 20 15.9706 20 11Z" stroke="currentColor" stroke-width="1.5" stroke-linejoin="round" />
                                </svg>
                            </button>
                        </form>
```
in this code we not write any thing in the form 
- - Code for the view.py is :- 
```
if request.GET.get('search'):
        search_term = request.GET.get('search')
        recipes = Recipe.objects.filter(name__icontains=search_term)
```
in this code we directly check the get methode (this is use only for the search and filter only)

- - ```__icontains``` is use to get , is that thing is contain or not
- - For example in this code , ```(name__icontains=search_term)``` icontain only check is this name is present or not

- # This time to add the authication system in the project ```Authentication```
- - We not need to add the user model in the project , because we already get the user model by django
- - So the code for it is :- 
```
from django.contrib.auth.models import User

class Recipe(models.Model):
    user = models.ForeignKey(User , on_delete=models.CASCADE , null=True , blank=True) # on delete cascade means after the deletion the user the user related all the records get deleted
    name = models.CharField(max_length=100)
    desc = models.TextField()
    image = models.ImageField(upload_to="Recipe_Image")

```
- - See we not need to make any user model in the webiste 
- - The view code the register and login is :- (this is also done by the django)
```
def register_form(request):
    if request.method == 'POST':
        name = request.POST.get('name')
        password = request.POST.get('password')
        if User.objects.filter(username=name).exists():
            messages.error(request, 'Username already exists')
            return redirect('register_form')
        user = User.objects.create_user(username=name, password=password)
        messages.success(request, 'Account created successfully')
        return redirect('login_form')
    return render(request, 'register.html')

def login_form(request):
    if request.method == 'POST':
        name = request.POST.get('name')
        password = request.POST.get('password')
        user = authenticate(request, username=name, password=password) 
        if user is not None:
            login(request, user)
            messages.success(request, 'Login successful')
            return redirect('recipe_form')
        else:
            messages.error(request, 'Invalid username or password')
            return redirect('login_form')
    return render(request, 'login.html')
```
```Note```
- - The authenticate function is a built-in Django function that checks the provided credentials against the user database. It returns:
1. A User object if the credentials are valid.
2. None if the credentials are invalid.
- - Login by the django is use as the session (means for a iterval you got login in the website and the website understand which one is gone to logged in)
- similarly code for the logout is :- 
```
def logout_form(request):
    logout(request)
    redirect('/login')

```
- - ```Login required``` in the login help in the requirement of the login for the webiste the code for it is :- 
```
from django.contrib.auth.decorators import login_required
@login_required(login_url='/login') # this will direct to that page where you want to redirect if he or she is not logined 
def recipe_form(request):
```

- ## Dynamic url in the webiste is :- 
- - This function is also provided by the login 
```
<div>
                {% if request.user.is_authenticated %}
                    <a href="logout/" class="inline-block bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded text-sm transition duration-300">Logout</a>
                {% else %}
                    <a href="login/" class="inline-block bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded text-sm transition duration-300 mr-2">Login</a>
                    <a href="register/" class="inline-block bg-gray-200 hover:bg-gray-300 text-gray-800 font-bold py-2 px-4 rounded text-sm transition duration-300">Register</a>
                {% endif %}
            </div>
```

- ## Advance ORM
- If we want to short the data according to the component value then , the code is :-
asending order:-
```Recipe.objects.all().order_by('component_value')```
desending order :- 
```Recipe.objects.all().order_by('-component_value')```
- If we have large amount , then we need less amount of data to come then the code is :- 
```Recipe.objects.all().[0  : 100] ``` #hundered records 
- If we want greater then or less then the specific value , then the code is :- 
greater then or equal to :- 
```Recipe.objects.all().filter(component_value__gte = value)```
less then or equal to :- 
```Recipe.objects.all().filter(component_value__lte = value)```

- ## Admin panel in the django 
- - got to '/admin/' for the admin panel 
- - It ask for the username and password , then go to terminal and write the code ```python manage.py createsuperuser```
- - Set all things 
- - Then after we have to resigter all the model in the admin panel (this is done throught the admin.py)
- - This is the model.py code 
``` 
class Department(models.Model):
    department = models.CharField(max_length=100)
```
and the code for the ``admin.py``
```admin.site.register(Department)```
- - Now we are ready to see the admin panel 

- ## str 
```
def __str__(self) -> str:
        return self.department
```
due to this code the object is showing as the name of the department
- ## Meta class in the model 





















- ## For the fake data we need the ```Faker ``` from the django 
```
from faker import Faker
fake = Faker()
name = fake.name()
email = fake.email()
address = fake.address()
phone = fake.phone()
```

- ## This is the time for the ```Advance query in the django ```
- - Assuning this data base is for the students 
- - If want that name of the student start with
```
 Student.objects.all().filter(student_name__startswith = 'a')
 ```
- - If want that name of the student start with
```
 Student.objects.all().filter(student_name__endswith = 'a')
 ```
- - If want that name of the student contains some letter then use this code 
```
 Student.objects.all().filter(student_name__icontains = 'a')
 ```
- - If want to search how many of them from the cse department then this code is gone to use :- 

```student.objects.all().filter(department__department = 'cse').count()```
first department is for the foreign key to get the object and second department after ```__``` is for the department of that department object
- - If we want that the student of the two department are :- 
```
d = ['CSE' , 'IT']
student = Student.objects.all().filter(department__department__in = d)
```
In this code the first department is for excess the first foreign key and the second for the name of the department and betweeb them ```__``` is for to go to one to another model and ```__in ```is for those department which is in the array of d 
- - If want that the cse student excludeed then wriet the code :- 
```
d = ['CSE']
student = Student.objects.all().exclude(department__department__in = d)
```
```filter meand include and exclude means exclude ```
- - If we want that to have a that is that exit or not then we write the code :- 
```
student = Student.objects.all().filter(student_name__icontains = 'a')
student.exit() 
```
If exit then it will return the true and not it will return false 
- - ```.value()``` will return the value of the object (only object) , and also for the excess we use the object js [] bracket methode for getting the valuees, code is 
```
student = Student.objects.all()
student.value()[0]['student_name']
```
- - If we want the reverse then write this code :- ```.reverse()```
- - If we want to get the specific amount of data then use the ```.value_list()``` the code for it is :- 
```student = Student.objects.values_list('student_name`)``` now this gone to give all the name to use 
- - ``get`` only gone to use when the data is must present in the data
- - ### The most advance part of the query is ```Aggregation and annotation``` 
- - - The code for the is aggreate:- 
The aggreate function is only work one the single column example it is only work for the model single column only not the other , but the filter is gone to work on the whole , but the aggreate function is working on the same column but for the whole data not for the single it gone to work for the whole colum of the data base realted to that column . Application of it is that like average or the sum of the marks or age of the student 
```
from django.db.models import *
Student.objects.aggregate(Avg('student_age'))
```
```similar do the Max , Min , Sum ```
- - - The code for the is :- 
The anotate is similar as the aggreate function but only chnage is that these gone to work on the two aggreate function (means it gone to work on the two values not on the single values)
``` student = Student.objects.values('department' , 'student_age').annotate(Count('department') , Count('student_age'))```
this will explain the code that department 1 how many people and student_age how many people. important is that it will give the intersection between the both depatments (means comman (means [particular age and department student count ]))
``` student = Student.objects.values('student_age').annotate(Count('student_age'))``` We can also use this for the single 
- ## Foreign key important 
- - The code for th models is :- 
```
class Department(models.Model):
    department = models.CharField(max_length=100)
    date = datetime.datetime

class Student(models.Model):
    department = models.ForeignKey(Department, related_name='students', on_delete=models.CASCADE)
    student_name = models.CharField(max_length=100)
```
- - Then how to excess the department object data :- 
the code is :- ```Student[0].department.date``` and ```Student[0].department.department```
- - Foreign key means one to many realtionship between the models of the department and students (single department and many students)

## Report card project
- ## Student and Subject and its mark beautiful combination 
- - The code for the models.py is :- 
- - 
```
class Student(models.Model):
    department = models.ForeignKey(Department, related_name='students', on_delete=models.CASCADE)
    student_id = models.OneToOneField(StudentId, related_name='student', on_delete=models.CASCADE)
    student_name = models.CharField(max_length=100)
    student_email = models.EmailField(max_length=100, unique=True)
    student_age = models.IntegerField()
    student_address = models.CharField(max_length=100)

    def __str__(self):
        return self.student_name

    class Meta:
        ordering = ['student_name']
        verbose_name = 'student'
        verbose_name_plural = 'students'

class Subject(models.Model):
    subject_name = models.CharField(max_length=100)

    def __str__(self):
        return self.subject_name

class SubjectMarks(models.Model):
    student = models.ForeignKey(Student, related_name='marks', on_delete=models.CASCADE)
    subject = models.ForeignKey(Subject, related_name='marks', on_delete=models.CASCADE)
    mark = models.IntegerField()

    def __str__(self):
        return f"{self.student.student_name} - {self.subject.subject_name}"

    class Meta:
        unique_together = ['student', 'subject']
```
This is the beautiful connvert of the``` simple one to many into many to many relationship``` , this is awssome , because student and subject are seperate but at the end of the code they get join and make the many to many relationship with the unique together(means student with same name canot have the same subject marks two times)
- - Fake code for it is :- 
```
from .models import Department, StudentId, Student , Subject , SubjectMarks
from faker import Faker
from random import randint

fake = Faker()

def fake_mark_data():
    students = Student.objects.all()
    for student in students:
        subjects = Subject.objects.all()
        for subject in subjects:
            marks = randint(0, 100)
            SubjectMarks.objects.create(student=student, subject=subject, marks=marks)
    print("Created subject marks for all students.")

def fake_student_data(n):
    departments = list(Department.objects.all())
    if not departments:
        print("No departments found. Please create some departments first.")
        return

    for i in range(n):
        student_depart = departments[randint(0, len(departments) - 1)]
        student_id_obj = StudentId.objects.create(studentid=f"STU{randint(100000, 999999)}")
        
        student_name = fake.name()
        student_email = fake.email()
        student_age = randint(18, 25)
        student_address = fake.address()

        student_data = Student.objects.create(
            student_id=student_id_obj,
            student_name=student_name,
            student_email=student_email,
            student_age=student_age,
            student_address=student_address,
            department=student_depart 
        )

        print(f"Created student {i+1}:")
        print(f"ID: {student_id_obj.studentid}")
        print(f"Name: {student_name}")
        print(f"Email: {student_email}")
        print(f"Age: {student_age}")
        print(f"Address: {student_address}")
        print(f"Department: {student_depart}")
        print("------------------------")

    print(f"Created {n} student records.")
```
- ## Custom admin panel small look is that :- 
- - See the code :- 
```
class SubjectMarkAdmin(admin.ModelAdmin):
    list_display = ['student' , 'subject' , 'mark']
admin.site.register(SubjectMarks , SubjectMarkAdmin)
```
In this code first make a new class for the admin using modeladmin and then after that add what we need to display and after that we gone to add that class with the SubjectMarks class in the admin.py

- ## Pagination in the website code 
- - code fo the views.py code  :- 
```
from django.core.paginator import Paginator

def student_data(request):
    query = Student.objects.all().order_by('student_id')
    paginator = Paginator(query , 12) 
    page_number = request.GET.get("page")
    page_obj = paginator.get_page(page_number)
    return render(request, 'student_data.html', {"page_obj": page_obj})
```
- - Now the code for the frontend is :- 
```
{% for contact in page_obj %}
    {# Each "contact" is a Contact model object. #}
    {{ contact.full_name|upper }}<br>
    ...
{% endfor %}

<div class="pagination">
    <span class="step-links">
        {% if page_obj.has_previous %}
            <a href="?page=1">&laquo; first</a>
            <a href="?page={{ page_obj.previous_page_number }}">previous</a>
        {% endif %}

        <span class="current">
            Page {{ page_obj.number }} of {{ page_obj.paginator.num_pages }}.
        </span>

        {% if page_obj.has_next %}
            <a href="?page={{ page_obj.next_page_number }}">next</a>
            <a href="?page={{ page_obj.paginator.num_pages }}">last &raquo;</a>
        {% endif %}
    </span>
</div>
```
and this is frontend code for the paginator

- ## Advanced search in the django with the ```Q```
- - Code for it is :- 
- - View code :- 
```
from django.shortcuts import render
from django.core.paginator import Paginator
from .models import Student
from django.db.models import Q

def student_data(request):
    query = Student.objects.all().order_by('student_id')
    if request.GET.get('search') :
        search = request.GET.get('search')
        query = query.filter(
            Q(student_name__icontains=search) |
            Q(student_email__icontains=search) |
            Q(student_id__studentid__icontains=search)|
            Q(department__department__icontains=search)
        )
    paginator = Paginator(query , 12) 
    page_number = request.GET.get("page")
    page_obj = paginator.get_page(page_number)
    return render(request, 'student_data.html', {"page_obj": page_obj})

```
- - The frontend code for it is :- 
```
<form >
            <input type="text" name="search" placeholder="search">
            <button>submit</button>
</form>
```
- ## Name in the url work 
- - 
```
<td class="px-6 py-4"><a href="/reportcard/{{student.student_id.studentid}}" class="underline">{{ student.student_id.studentid }}</a></td>

<td class="px-6 py-4"><a href="{% url 'student_marks' student.student_id.studentid %}" class="underline">{{student.student_id.studentid }}</a></td>
```
This both code is same , there working is same 
- - The url code is :- 
```
path('reportcard/<student_id>', student_marks , name='student_marks'),
```
- - The main application of the url is that it will work if the url '/ slask value gone to change'

- ## Related name in the foreign key importance
- - ## ```Means reverse excess ```
- - see the code before :- 
```
class Subject(models.Model):
    subject_name = models.CharField(max_length=100)

    def __str__(self):
        return self.subject_name

class SubjectMarks(models.Model):
    subject = models.ForeignKey(Subject, related_name='marks', on_delete=models.CASCADE)
    mark = models.integerfield()
```
- - This is code of the one to many relations ship (in this if i use the subjectmarks class and want to excess the suject then the code is``` subjectmarks.subject.subject_name```)
- - And i want to excess the mark and in the subject class then we can do throught the related name marks , the code is ```subject.marks.mark ```


- ## Important note 
- - If we want to go to class to its element data then we use ```__```  and ```.``` , ```__``` is use in the database query of the sql and the ```.``` is use in the normal code 



- ## Diffrence between the ```"filter"``` and the``` "get"```
- - ```Filter ``` must return a query set means a array of object (else it is empty or the single value but it is continue as the array)
-- ```get``` but the get 
1. Returns a single object that matches the given criteria.
2. If multiple objects match, it raises a MultipleObjectsReturned exception.
3. If no object matches, it raises a DoesNotExist exception.
- - So when we use the ```get``` we need some time for and some time not required
- - But when we use the ```filter``` then we must required  the for loop to use in the templates (weather there is single or multiple or none object)
- - The code for the first case is :- 
```
def student_marks(request, student_id):
    marks = SubjectMarks.objects.all().filter(student__student_id__studentid=student_id)
    student = Student.objects.all().filter(student_id__studentid=student_id)
    return render(request, 'student_marks.html' , {"marks" : marks , "students" : student})
```
```
{% for student in students %}
                    <tr class="border-b">
                        <th class="text-left py-2 px-4 font-semibold text-gray-600">Student ID:</th>
                        <td class="py-2 px-4 text-gray-800">{{student.student_id.studentid}}</td>
                    </tr>
                    <tr class="border-b">
                        <th class="text-left py-2 px-4 font-semibold text-gray-600">Name:</th>
                        <td class="py-2 px-4 text-gray-800">{{student.student_name}}</td>
                    </tr>
                    <tr class="border-b">
                        <th class="text-left py-2 px-4 font-semibold text-gray-600">Email:</th>
                        <td class="py-2 px-4 text-gray-800">{{student.student_email}}</td>
                    </tr>
                    <tr class="border-b">
                        <th class="text-left py-2 px-4 font-semibold text-gray-600">Age:</th>
                        <td class="py-2 px-4 text-gray-800">{{student.student_age}}</td>
                    </tr>
                    <tr>
                        <th class="text-left py-2 px-4 font-semibold text-gray-600">Department:</th>
                        <td class="py-2 px-4 text-gray-800">{{student.department.department}}</td>
                    </tr>
                    {% endfor %}
```
- - The above code is for the single student but we will use the for loop 
- - The code for the second case is :- 
```
def student_marks(request, student_id):
    marks = SubjectMarks.objects.all().filter(student__student_id__studentid=student_id)
    student = Student.objects.get(student_id__studentid=student_id)
    return render(request, 'student_marks.html' , {"marks" : marks , "student" : student})

<tbody>
                    <tr class="border-b">
                        <th class="text-left py-2 px-4 font-semibold text-gray-600">Student ID:</th>
                        <td class="py-2 px-4 text-gray-800">{{student.student_id.studentid}}</td>
                    </tr>
                    <tr class="border-b">
                        <th class="text-left py-2 px-4 font-semibold text-gray-600">Name:</th>
                        <td class="py-2 px-4 text-gray-800">{{student.student_name}}</td>
                    </tr>
                    <tr class="border-b">
                        <th class="text-left py-2 px-4 font-semibold text-gray-600">Email:</th>
                        <td class="py-2 px-4 text-gray-800">{{student.student_email}}</td>
                    </tr>
                    <tr class="border-b">
                        <th class="text-left py-2 px-4 font-semibold text-gray-600">Age:</th>
                        <td class="py-2 px-4 text-gray-800">{{student.student_age}}</td>
                    </tr>
                    <tr>
                        <th class="text-left py-2 px-4 font-semibold text-gray-600">Department:</th>
                        <td class="py-2 px-4 text-gray-800">{{student.department.department}}</td>
                    </tr>
                </tbody>
```
- - In the above code there is no need of the for loop because it return single object 

- ## Rank generation in the project of the report card 
- - First methode is to generate rank each time of load or the call of the function .The code is :- 
```
    rank = -1 
    ranks = Student.objects.annotate(student_mark = Sum('marks__mark')).order_by('-student_mark' , '-student_age')
    i = 1
    for student in ranks:
        if student.student_id.studentid == student_id:
            rank = i
            break
        i = i + 1
```
- - Seocond code methode is to make a rank and store in the database . The code for the whole process is :- 

- ## We know that the django provide the default user  and if we want to customize it (using model manager) and if we want to admin panel login through the phone number in place of the username and  want to add more thing in that ,  then do this 
- - There are two methode for the ccustome user model :- 
- - 1. Abstract methods (all default things + new custom)
- - 2. Abstract base methods (username + password + only new custom)
- - Write the custome model manager useing abstract methods 
- - - Models.py 
```
from django.contrib.auth.models import AbstractUser
from .manager import UserManager

# This is code for the custome user model 
class CustomUser(models.Model):
    #provide by the django default user model
    username = None # this is for not to take a username 
    email = models.EmailField(unique=True)
    #add new things to it like phone_no (because use the abstract model)
    phone_no = models.CharField(max_length=15)
    profile_picture = models.ImageField(upload_to='profile_pics/', null=True, blank=True)
    bio = models.TextField(max_length=500, blank=True)
    followers = models.ManyToManyField(settings.AUTH_USER_MODEL, related_name='following', blank=True)

    objects = UserManager()

    # This is for those to take email at the place of the login in the admin panel in place of the username 
    USERNAME_FIELD = 'email' 
    REQUIRED_FIELD = []

    #we not get the defaultmodel manage in the abstract model so we make a model manager name manager.py
```
- - - Model Manager code 
```
# this helps in the query of the database
# objects is is the model manager (which help in the query of the database)

from django.contrib.auth.base_user import BaseUserManager

class UserManager(BaseUserManager): # inherite all the default model manager of the django 
    use_in_migrations = True # this is for to use this custom model manager at the  place of the default model manager 

    def create_user(self , email , password = None , **extra_fields):
        if not email:
            raise ValueError("Email is required")
        user = self.model(email = email , **extra_fields)
        user = self.normalize_email(email)
        user.set_password(password)
        user.save(using = self._db)
        return user

    def create_superuser(self , email , password , **extra_fields):
        extra_fields.setdefault('is_staff', True)
        extra_fields.setdefault('is_superuser', True)
        extra_fields.setdefault('is_active', True)

        return self.create_user(self , email , password , **extra_fields)
```
- - The code for the setting.py is :- 
```
ALLOWED_HOSTS = []
AUTH_USER_MODEL = 'others.CustomUser'
```
- - Now for createing user and super user write this code :- 
```python manage.py createuser or createsuperuser```
in the termial to make a super user and create user in the termial 

- Now we not need any type of abstracte base model (becuase abstracte model is enough)

- ## Model manager 
- - we now ```objects``` is the model manager 
- - Now we know that if we want to excess the some specific then we use the filter code like
``` student.objects.all().filter(student_name__icontains = 'a')```
now we need not write the such big things 
- - If I only want those student whose is_deleted is fasle (then we no need to write such big filter code like above) 
- - The code for the models class is :- 
- - 
```
#this is code for the model manager
class StudentModelManager(models.Manager): # take default model manager
    def get_query(self):
        return super().get_queryset().filter(is_deleted = True)

#this is code for the model class
class Student(models.Model):
    student_name = models.CharField(max_length=100)
    is_deleted = models.BooleanField(default=false)

    objects = StudentModelManager()
    admin_objects = models.Manager() # this is the default manager given by the admin  # means admin is able to see all 
```
- - After this code when we write the code :- 
```Student.objects.all()``` now this code will give the only those student which is gone to deletd 
```Student.admin_objects.all()```now this code will give the all student because admin is useing the default model manager 

## How to send the email using the django 
- First code is for the simple  send email :-  
- - Setting py code for it is :- 
```
EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
EMAIL_HOST = 'smtp.gmail.com'  # Replace with your SMTP server
EMAIL_PORT = 587
EMAIL_USE_TLS = True
EMAIL_HOST_USER = 'hello01world012000@gmail.com'
EMAIL_HOST_PASSWORD =  'qeuo pvut jywa jmkb'
```
and the code for the utils.py is :- 
```
from django.core.mail import send_mail
from django.conf import settings

def send_email_to_user():
    subject = 'Welcome to My Website'
    message = 'This is a test email.'
    from_email = settings.EMAIL_HOST_USER 
    recipient_list = ['ayushchaurasia08102006@gmail.com']
    send_mail(subject, message, from_email , recipient_list)
    print('Email sent successfully')
```
- Second code is for the advanced send email with the file attachment :- 
- - setting .py code is same 
- - utils code is :- 
```
from django.core.mail import send_mail , EmailMessage
from django.conf import settings
import os 

def send_email_to_user_with_attachment():
    subject = 'Welcome to My Website'
    message = 'This is a test email with attachment.'
    from_email = settings.EMAIL_HOST_USER
    recipient_list = ['ayushchaurasia08102006@gmail.com']
    file_path =  os.path.join(settings.BASE_DIR, "Screenshot_2.png")

    mail = EmailMessage(subject=subject , body=message , from_email=from_email, to=recipient_list)
    mail.attach_file(file_path)
    mail.send()
    print('Email sent successfully with attachment')
```

## Signal in the django 
- Signal means when the class is gone to made then the function is gone to automatically called 
- Signal is of four type :- 
1. pre_save (activity done before the data gone to save)
2. post_save (activity done after the data save)
3. pre_delete (similar as  the above)
4. post_delete 
-  Here i am using post_save means this function is gone to call after each data save 
- The code for it is :- 
```
from django.db.models.signals import post_save
from django.dispatch  import receiver

class Student(models.Model):
    name = models.CharField(max_length=100)

@receiver(post_save, sender=Student) # now this function is gone to call after each student data gone to save
def create_student_id(sender, instance, created, **kwargs):
    print('Student saved successfully')
    print(sender , instance , kwargs)
```
- Note , this is use to give the recored for the those who gone to change the data and when gone to change

## Thread (same as the celery (the task is done in the background))
- Those task which take more time then we use the concept of the thread because we gone to do those task in the background 
- So long process is gone to done under the thread so the other work is gone to continue 
- The example code is :- 
- The code for it is :- 
```
import threading
import time
from django.core.mail import send_mail
from django.conf import settings

# Email sending through thread
class SendEmail(threading.Thread):
    def __init__(self, recipient_list, subject, message):
        self.recipient_list = recipient_list
        self.subject = subject
        self.message = message
        threading.Thread.__init__(self)

    def run(self):
        time.sleep(10)  # this is to simulate a delay
        try:
            send_mail(
                subject=self.subject,
                message=self.message,
                from_email=settings.EMAIL_HOST_USER,
                recipient_list=self.recipient_list
            )
            print('Email sent successfully')
        except Exception as e:
            print(f'Error sending email: {e}')

# Function to create and start the email thread
def send_email_async(recipient_list, subject, message):
    email_thread = SendEmail(recipient_list, subject, message)
    email_thread.start()
    return email_thread
```
- Above is the user resgisteration application for the greeting 
- other app;ication are :- 
1. external api call 
2. data processing
3. sending email to many ones 
```
def send_mass_email(mass_email_content):
    subscribers = Subscriber.objects.all()
    for subscriber in subscribers:
        send_email_async([subscriber.email], 'mass_email', mass_email_content)
```

## Custom ui in the django 
- For the custom ui in the admin panel in the django we can use the ```'jazzmin'```
- Installing code for it is :- 
```
pip install django-jazzmin
pip install django-admin-interface
```
- Installed app code :- 
```
INSTALLED_APPS = [
    'jazzmin',
    'django.contrib.admin',
    # ... other apps
]

# Jazzmin settings
JAZZMIN_SETTINGS = {
    # ... jazzmin settings here
}
```
- Url code is no change need
```
from django.urls import path
from django.contrib import admin

urlpatterns = [
    path('admin/', admin.site.urls),
]
```

## Corn job (corntab) in the django (is similar as the celery (is the giant thing) , but the corn job is the small things like threads)
- Sorry for that the corn job is not gone to sported in the window 
- The top alternative of the corn job is ```apscheduler```
- Installing code is :-  ```pip install apscheduler django-apscheduler```
- Installed setting code 
```
INSTALLED_APPS = [
    ...
    no need to add anything the installed app
    ...
]
```
-  
```
from apscheduler.schedulers.background import BackgroundScheduler
import random

def print_random_number():
    print(f"Random number: {random.randint(1, 100)}")

def start():
    scheduler = BackgroundScheduler()
    scheduler.add_job(print_random_number, 'interval', seconds=10)
    scheduler.start()
    print("Scheduler started...")
```
In this code first import the background scheduler and  in the  def start , first run the background scheduler and then add the job to  the  background scheduler and  then  start the background scheduler
-  For  the running the background scheduler in the ```apps.py```   extra write the code 
```
def ready(self):
        from . import scheduler
        scheduler.start()
```

## What is the apps.py  work in the code  :- 
- The apps.py file in a Django app is used to configure app-specific settings. The code in this file, particularly the AppConfig subclass, is ```automatically loaded when Django starts.```

## Django sending otp using the django 
- I am using the twillio for the sending the otp verification code 
- Verification code is :- 
- Setting.py code :- 
```
# For otp verifications 
# TWILIO_ACCOUNT_SID = ""
# TWILIO_AUTH_TOKEN = ''
# TWILIO_PHONE_NUMBER = ''
```
- Models code is :- 
```
# from django.db import models
# from django.contrib.auth.models import User
# import random
# class PhoneVerification(models.Model):
#     user = models.OneToOneField(User, on_delete=models.CASCADE)
#     phone_number = models.CharField(max_length=15)
#     otp = models.CharField(max_length=6)
#     is_verified = models.BooleanField(default=False)

#     def generate_otp(self):
#         self.otp = str(random.randint(100000, 999999))
#         self.save()

#     def verify_otp(self, otp):
#         if self.otp == otp:
#             self.is_verified = True
#             self.save()
#             return True
#         return False
```
- View.py code is :- 
```
# from django.shortcuts import render, redirect
# from django.conf import settings
# from twilio.rest import Client
# from .models import PhoneVerification
# from django.contrib.auth.models import User

# def send_otp(request):
#     if request.method == 'POST':
#         username = request.POST.get('username')
#         email = request.POST.get('email')
#         password = request.POST.get('password')
#         phone_number = request.POST.get('phone_number')

#         # Ensure the phone number is in international format for India
#         if not phone_number.startswith('+'):
#             phone_number = '+91' + phone_number.lstrip('0')

#         # Create user
#         try:
#             user = User.objects.create_user(username=username, email=email, password=password)
#         except Exception as e:
#             return render(request, 'send_otp.html', {'error': f'Failed to create user: {str(e)}'})

#         # Create or get PhoneVerification instance
#         phone_verification, created = PhoneVerification.objects.get_or_create(user=user)
#         phone_verification.phone_number = phone_number
#         phone_verification.generate_otp()

#         # Twilio client setup
#         client = Client(settings.TWILIO_ACCOUNT_SID, settings.TWILIO_AUTH_TOKEN)

#         try:
#             message = client.messages.create(
#                 body=f"Hello sir , Your OTP is: {phone_verification.otp}",
#                 from_=settings.TWILIO_PHONE_NUMBER,
#                 to=phone_number
#             )
#             print(f"SMS sent successfully. SID: {message.sid}")
#             return redirect('verify_otp')
#         except Exception as e:
#             # If SMS sending fails, delete the created user
#             user.delete()
#             print(f"Error sending SMS: {str(e)}")
#             return render(request, 'send_otp.html', {'error': f'Failed to send OTP: {str(e)}'})

#     return render(request, 'send_otp.html')

# def verify_otp(request):
#     if request.method == 'POST':
#         otp = request.POST.get('otp')
#         phone_verification = PhoneVerification.objects.get(user=request.user)
#         if phone_verification.verify_otp(otp):
#             return render(request, 'verification_success.html')
#         else:
#             return render(request, 'verify_otp.html', {'error': 'Invalid OTP'})
#     return render(request, 'verify_otp.html')
```
