# Getting Started with App Engine

## Overview

You will create and deploy a simple App Engine application using a virtual environment in the Google Cloud Shell.
## Objectives

You will be performing the following tasks:

-   Initialize App Engine.
    
-   Preview an App Engine application running locally in Cloud Shell.
    
-   Deploy an App Engine application, so that others can reach it.
    
-   Disable an App Engine application, when you no longer want it to be visible.
first , you activate the cloud shell
You can list the active account name with this command:

```
gcloud auth list

```

You can list the project ID with this command:

```
gcloud config list project

```

## Step 1: Initialize App Engine

1.  Initialize your App Engine app with your project and choose its region:
    
    ```
    gcloud app create --project=$DEVSHELL_PROJECT_ID
    
    ```
    
    When prompted, select the region where you want your App Engine application located or close too.
    
2.  Clone the source code repository for a sample application in the  **hello_world**  directory:
    
    ```
    git clone https://github.com/GoogleCloudPlatform/python-docs-samples
    
    ```
    
3.  Navigate to the source directory:
    
    ```
    cd python-docs-samples/appengine/standard_python3/hello_world
    
    ```
    

## Step 2: Run Hello World application locally
You will run the Hello World application in a local, virtual environment in Cloud Shell.
1.  Execute the following command to download and update the packages list.
    
    ```
    sudo apt-get update
    
    ```
    
2.  Set up a virtual environment in which you will run your application. Python virtual environments are used to isolate package installations from the system.
    
    ```
    sudo apt-get install virtualenv
    
    ```
    
    If prompted [Y/n], press  `Y`  and then  `Enter`.
    
    ```
    virtualenv -p python3 venv
    
    ```
    
3.  Activate the virtual environment.
    
    ```
    source venv/bin/activate
    
    ```
    
4.  Navigate to your project directory and install dependencies.
    
    ```
    pip install  -r requirements.txt
    
    ```
    
5.  Run the application:
    
    ```
    python main.py
    
    ```
    

Please ignore the warning if any.

6.  In  **Cloud Shell**, click  **Web preview**    **Preview on port 8080**  to preview the application.

To access the  **Web preview**  icon, you may need to collapse the  **Navigation menu**.

## Step 3: Deploy and run Hello World on App Engine

Deploy your application to the App Engine Standard environment:

1.  Navigate to the source directory:
    
    ```
    cd ~/python-docs-samples/appengine/standard_python3/hello_world
    
    ```
    
2.  Deploy your Hello World application.
    
    ```
    gcloud app deploy
    
    ```
    

If prompted "Do you want to continue (Y/n)?", press  `Y`  and then  `Enter`.

This  **app deploy**  command uses the  _app.yaml_  file to identify project configuration.

3.  Launch your browser to view the app at http://YOUR_PROJECT_ID.appspot.com
    
    ```
    gcloud app browse
    
    ```
    

Copy and paste the URL into a new browser window.
## Task 4: Disable the application

App Engine has no option to  **Undeploy**  an application.However, you can disable the application, which causes it to no longer be accessible to users.

1.  In the Cloud Console, on the  **Navigation menu** , click  **App Engine**  >  **Settings**.
    
2.  Click  **Disable application**.
3. You are done setting up app engine