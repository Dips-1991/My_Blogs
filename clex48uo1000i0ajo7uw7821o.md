---
title: "Day-13 Task: Basics of Python"
datePublished: Mon Mar 06 2023 17:48:33 GMT+0000 (Coordinated Universal Time)
cuid: clex48uo1000i0ajo7uw7821o
slug: day-13-task-basics-of-python
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1678124603020/482acce0-ad19-49b3-bd1c-2eb76165d5cf.jpeg
tags: aws, python3, python-beginner, devops-journey, pythondatatypes

---

**What is Python Programming Language?**

Python is a high-level, general-purpose, and very popular programming language. Python programming language (latest Python 3) is being used in web development, Machine Learning applications, along with all cutting-edge technology in Software Industry. Python Programming Language is very well suited for Beginners, also for experienced programmers with other programming languages like C++ and Java.

It was created by `Guido van Rossum`

The biggest strength of Python is huge collection of standard libraries which can be used for the following:

* Machine Learning
    
* GUI Applications (like [Kivy](https://www.geeksforgeeks.org/kivy-tutorial/), Tkinter, PyQt etc. )
    
* Web frameworks like [Django](https://www.geeksforgeeks.org/django-tutorial/) (used by YouTube, Instagram, Dropbox)
    
* Image processing (like [OpenCV](https://www.geeksforgeeks.org/opencv-python-tutorial/), Pillow)
    
* Web scraping (like Scrapy, BeautifulSoup, Selenium)
    
* Test frameworks
    
* Multimedia
    
* Scientific computing
    
* Text processing and many more...
    

**How to Install Python?**

You can install Python in your System whether it is Windows, MacOS, ubuntu, centos, etc. Below are the links for the installation:

[Python Installation](https://www.python.org/downloads/)

Here we will install Python3 in the Ubuntu OS

**Task:1**

1. **Install Python in your respective OS, and check the version.**
    
    To install python in ubuntu use the below command
    
    `sudo apt-get install -y python3`
    
    To check version
    
    `python3 --version`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678116941798/ed28d30c-3dfd-4247-8bb1-f4e449258f30.png align="center")
    
2. **Data Types in python**
    
    Data types are the classification or categorization of data items. It represents the kind of value that tells what operations can be performed on a particular data. Since everything is an object in Python programming, data types are actually classes and variables are instances (objects) of these classes.
    
    Following are the standard or built-in data types of Python:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678117757674/ba0ac416-d06b-432c-9ddc-36c91cd87099.jpeg align="center")
    
    1. **Numeric Data Type:**
        
        In Python, numeric data type represent the data which has numeric value. Numeric value can be integer, floating number or even complex numbers. These values are defined as `int`, `float` and `complex` class in Python.
        
        * `integers` – This value is represented by int class. It contains positive or negative whole numbers (without fractions or decimals). In Python, there is no limit to how long an integer value can be.
            
        * `Float` – This value is represented by the float class. It is a real number with a floating-point representation. It is specified by a decimal point. Optionally, the character e or E followed by a positive or negative integer may be appended to specify scientific notation.
            
        * `Complex Numbers` – Complex number is represented by a complex class. It is specified as *(real part) + (imaginary part)j*. For example – 2+3j
            
            ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678118657596/2537a193-533e-4c2a-9ad4-9699748051e1.png align="center")
            
    2. **Sequence Data Type:**
        
        In Python, sequence is the ordered collection of similar or different data types. Sequences allows to store multiple values in an organized and efficient fashion. There are several sequence types in Python –
        
        * `String` - In Python, **Strings** are arrays of bytes representing Unicode characters. A string is a collection of one or more characters put in a single quote, double-quote or triple quote. In python there is no character data type, a character is a string of length one. It is represented by `str` class.
            
            **Creating String-**
            
            Strings in Python can be created using single quotes `' '` or double quotes `" "` or even triple quotes.`""" """`
            
            ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678119328106/aa3d886d-c7bf-429f-be19-9e25f7080f0b.png align="center")
            
        * `List` - **Lists** are just like the arrays, declared in other languages which is an ordered collection of data. It is very flexible as the items in a list do not need to be of the same type.  
            **Creating List-**
            
            Lists in Python can be created by just placing the sequence inside the square brackets`[]`.
            
            ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678120312040/111038b4-882e-4436-918c-028fe2dbbb38.png align="center")
            
        * `Tuple`**\-** Just like list, **tuple** is also an ordered collection of Python objects. The only difference between tuple and list is that tuples are immutable i.e. tuples cannot be modified after it is created. It is represented by `tuple` class.
            
            **Creating List-**
            
            Lists in Python can be created by just placing the sequence inside the round brackets`()`.
            
            ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678121221226/95b265a0-b914-406e-b598-87a9c5910d5b.png align="center")
            
    3. **Boolean Data Type:**
        
        Data type with one of the two built-in values, `True` or `False`. Boolean objects that are equal to True are truthy (true), and those equal to False are falsy (false).
        
        **Note** – True and False with capital ‘T’ and ‘F’ are valid booleans otherwise python will throw an error.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678121857290/7a319498-fa05-4616-95f3-50b24a9fbeb9.png align="center")
        
    4. **Set:**
        
        In Python, a **Set** is an unordered collection of data type that is iterable, mutable, and has no duplicate elements. The order of elements in a set is undefined though it may consist of various elements.
        
        **Creating Sets-**
        
        Sets can be created by using the built-in `set()` function
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678122979043/610bba80-1859-4383-81e4-fb71f180422f.png align="center")
        
    5. **Dictionary:**
        
        Python Dictionary is an unordered sequence of data of key-value pair form. It is similar to the hash table type. Dictionaries are written within curly braces in the form `key:value`. It is very useful to retrieve data in an optimized way among a large amount of data.
        
        **Creating Dictionary-**
        
        In Python, a Dictionary can be created by placing a sequence of elements within curly `{}` braces, separated by ‘comma’.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678123793515/59d518f3-9412-4ce1-964d-95514c7265f9.png align="center")
        

Thank you for reading the article

Happy Learning!