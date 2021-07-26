Django Rest Framework Assignment 2

Assignment:
To create a simple registration API with proper validations using Django REST Framework.

Steps:
1. Create a Django App
2. Create a Serializer 'UserSerializer' which is inheriting from a ModelSerializer
3. The Serializer will have 3 attributes email which is a EmailField, username which is a Charfield and password field which is also a CharField
4. Make fields username and email as unique by using UniqueValidator from rest_framework.validators https://www.django-rest-framework.org/api-guide/validators/#uniquevalidator
5. For password make minium length as 6 
6. Set max length of username to 32
7. Add a create method to save User object
8. In Meta class for UserSerializer, add model as User and fields as -> 'id', 'username', 'email', 'password'
9. Urls
    1. Name in Django URL -> name is used for accessing that URL from your Django / Python code.
    2. For example you have this in 'student/urls.py
    3. url(r'^main/', views.main, name='main')
    4. In point 2, "main" is the name of this URL
    5. URL namespaces -> URL namespaces allow you to uniquely reverse named URL patterns even if different applications use the same URL names. At Line 21 in school/urls.py, path('student/', include(('student.urls', 'student'), namespace='student')),
    6. namespace='student is set. Remember, Both Name and Namespace are important for the assignment
    7. For this assignment's test cases we have used some predefined names and namespace
    8. Those names are defined below in the problem statement describes as "Django Url name"
    9. Please make sure you use those names in Django URLs or else your assignment's test will fail Summary: Namespace is "'student" set in school/urls.py file  and name is to be set for each URL in 'student/urls which is stated in the problem statement
10. For Views

    1. Create a class based or method based view which handles POST method
    2. Steps 1: Pass the request Input through UserSerializer and save it.
    3. Make sure you check if serializer is valid using is_valid() function. Return serializer.errors with code 400 if there is a error with serializer data
    4. Step 2: Use model Token imported from from rest_framework.authtoken.models
    5. Create a Token Object using User Serializer output
    6. Append Token.key generated from Token object to UserSerializer Output and Return it with 201 status


### Registration API

Django URL name: registration<br />

Actions:<br />

POST : Create a User with Token 

1. Create a user

```
      /users/  -d "username=rahul&email=rahul@gmail.com&password=rahul134"
      Response : {"id":2,"username":"rahul","email":"rahul@gmail.com","token":"09539e42fef9663bad61f53d41733b2bc8ef085e"}
      Response Code : 201
  ```
2. Create a user with short password
```
      /users/  -d "username=rahul&email=rahul@gmail.com&password=rahul134"
      Response : {"password":["Ensure this field has at least 6 characters."]}
      Response Code : 400
```

3. Create a User with no password
```
      /users/  -d "username=rahul&email=rahul@gmail.com&password="
      Response : {"password":["This field may not be blank."]}
      Response Code : 400
```
4. Create a USer with long username
```
      /users/  -d "username=rahulrahulrahulrahulrahulrahulrahulrahulrahulrahulrahulrahulrahulrahulrahulrahulrahul&email=rahul@gmail.com&password=rahul134"
      Response : {"username":["Ensure this field has no more than 32 characters."]}
      Response Code : 400
```
5. Create a User with no username
```
      /users/  -d "username=&email=rahul@gmail.com&password=rahul134"
      Response : {"username":["This field may not be blank."]}
      Response Code : 400
```
6. Create a User with existing username -> rahul user already exist
```
      /users/  -d "username=rahul&email=rahul@gmail.com&password=rahul134"
      Response : {"username":["This field must be unique."]}
      Response Code : 400
```
7. Create a User with existing email -> rahul@gmail.com user already exist
```
      /users/  -d "username=rahul&email=rahul@gmail.com&password=rahul134"
      Response : {"email":["This field must be unique."]}
      Response Code : 400
```
8. Create a User with Invalid email
```
      /users/  -d "username=rahul&email=hellopassword=rahul134"
      Response : {"email":["Enter a valid email address."]}
      Response Code : 400
```
9. Create a User with no email
```
      /users/  -d "username=rahul&email=&password=rahul134"
      Response : {"email":["This field may not be blank."]}
      Response Code : 400
```

NOTE: DO NOT CREATE ANY MODEL


Second API code need to be added ....
