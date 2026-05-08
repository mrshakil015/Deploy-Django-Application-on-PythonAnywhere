# Deploy-Django-Application-on-PythonAnywhere
![0.png](/images/0.png)
## Context
- [STEP 1: Prepare Your Django Project (Locally)](#step-1-prepare-your-django-project-locally)
    - [1. Update settings.py](#1-update-settingspy)
    - [2. Configure ALLOWED_HOSTS](#2-configure-allowed_hosts)
    - [3. Static Files Setup (Important)](#3-static-files-setup-important)
- [STEP 2: Create PythonAnywhere Account](#step-2-create-pythonanywhere-account)
- [STEP 3: Upload Your Project](#step-3-upload-your-project)
    - [Option A: Upload Zip File](#option-a-upload-zip-file)
    - [Option B: Clone from GitHub](#option-b-clone-from-github)
- [STEP 4: Create a Web App](#step-4-create-a-web-app)
- [STEP 5: Database Setup](#step-5-database-setup)
- [If You Fetch Permission issue](#note-if-you-fetch-any-permission-issue)

## **STEP 1: Prepare Your Django Project (Locally)**

Before uploading, make sure your project is production-ready.

### **1. Update `settings.py`**

```python
DEBUG = False
```

### **2. Configure `ALLOWED_HOSTS`**

You can set allowed host 2 way:

1. Used `pythonanywhere` domain name
    
    ```python
    ALLOWED_HOSTS = ['pythonanywhere_yourusername.pythonanywhere.com']
    ```
    
    Example: Change the `pythonanywhere_yourusername` based on your username
    
    ```python
    ALLOWED_HOSTS = ['mrshakil015.pythonanywhere.com']
    ```
    
2. You can allowed all
    
    ```python
    ALLOWED_HOSTS = ['*']
    ```
    

### **3. Static Files Setup (Important)**

Update [`settings.py`](http://settings.py) and Make sure you have:

```python
import os

STATIC_URL = '/static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'static')

MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
```

# STEP 2: Create PythonAnywhere Account

1. Go to 👉 [https://www.pythonanywhere.com](https://www.pythonanywhere.com/)
2. Create account
3. Login

# STEP 3: Upload Your Project

You can upload file on PythonAnyWhere using two ways:

A. Upload Manually from Files Tab

B. Clone Repository from github

> `Note:` Before upload file remove the all existing file form the **Files Tab.** You can remove it manually or from the console.
> 
> 
> ![1.png](/images/1.png)
> 
> **Remove the file using console:**
> 1. Go to **Consoles → Bash**
> 
> 2. And run the bellow command
> 
> ```bash
> rm -rf ~/*
> rm -rf ~/.??*
> ```
> 

### Option A: Upload Zip File

1. Zip the project folder on your local machine
2. Upload files from Files tab
    
    ![2.png](/images/2.png)
    
3. Go to **Consoles → Bash**  to unzip the file.
4. Unzip `.rar` file
    
    ```bash
    unrar x filename.rar
    ```
    
5. Unzip `.zip` file
    
    ```bash
    unzip filename.zip
    ```
    

### Option B: Clone from GitHub

```bash
git clone your_repo_url
cd your_project_folder
```

# STEP 4: Create a Web App

1. Go to **Dashboard**
2. Click **Web** Tab
3. Click `Add a new web app` button
    
    ![3.png](/images/3.png)
    
4. Then click Next
5. Then select `Manual Configuration` from Web framework section
    
    ![4.png](/images/4.png)
    
6. After that, Select the django version
7. Then click next button.
8. After that wait little bit to setup the web app.
9. Now on the web app tab scroll down and find `source code` section, here add your source code directory path. You can find it on the `Files` tab.
    
    ![5.png](/images/5.png)
    
    1. On the file tab click the the project folder.
        
        ![6.png](/images/6.png)
        
    2. Then copy the path and paste it on the source code.
        
        ![7.png](/images/7.png)
        
        ![8.png](/images/8.png)
        
10. Also find `WSGI configuration file` and edit this
    
    ![9.png](/images/9.png)
    
11. From the wsgi file remove all the code and place below code:
    
    ```bash
    import os
    import sys
    
    # add your project directory to the sys.path
    project_home = '/home/your_username/your_project_folder'
    if project_home not in sys.path:
        sys.path.insert(0, project_home)
    
    # set environment variable to tell django where your settings.py is
    os.environ['DJANGO_SETTINGS_MODULE'] = 'your_projectname.settings'
    
    # serve django via WSGI
    from django.core.wsgi import get_wsgi_application
    application = get_wsgi_application()
    ```
    
    `Note:` Replace the text  `your_username` ,  `your_project_folder` and `your_projectname` with the corrected name.
    
12. Then save the file.
13. Then Scroll down and Go To the Static Files section and add the media file route. Like below
    
    ![10.png](/images/10.png)
    
    To find this like go the the media folder on your main project directory then copy it.
    
    ![11.png](/images/11.png)
    
    `Note:` If you have static file directory also add the static file url same as media file
    
14. Also Add Static file root.
    
    ![12.png](/images/12.png)
    
    `Note:` Without run the `python manage.py collectstatic` you cannot find the `static or staticfile` folder. Also without run the `collectstatic` Django admin panel design not visible.
    
    Without run the `collectstatic`
    
    ![13.png](/images/13.png)
    
    After run `collectstatic`
    
    ![14.png](/images/14.png)
    
15. If you want you can enable HTTPS
    
    ![15.png](/images/15.png)
    

## STEP 5: Database Setup

PythonAnywhere free plan only supports **SQLite** easily.
If you upload full fresh project without any existing database or migrations file. You need to apply makemigrations and migrate. Also if you do any changes on your database you need to apply makemigrations and migrate.

> But there have a problem on PythonAnyWhere. You cannot apply migrations. You can fetch `permission denied` error.
> 
> 
> ![16.png](/images/16.png)
> 
> To solve this error set the full permission of your project using bellow command. 
> 
> ```bash
> chmod -R 755 ~/your_project_name
> ```
> 
> You can apply this command any permission denied type error.
> 

Then apply makemigrations and migrate command

```bash
python manage.py makemigrations app_name
```

```bash
python manage.py migrate
```

Now your website is live. To check click this link from the Web Tab

![17.png](/images/17.png)

## Note: If You Fetch Any Permission issue

To solve the permission error set the full permission of your project using bellow command. 

```bash
chmod -R 755 ~/your_project_name
```