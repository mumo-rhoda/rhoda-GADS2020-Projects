## In this lab, you create and deploy a simple App Engine application using a virtual environment in the Google Cloud Shell.

Objectives
 In this lab, you learn how to perform the following tasks:

    -Initialize App Engine.
    -Preview an App Engine application running locally in Cloud Shell
    -Deploy an App Engine application, so that others can reach it.
    -Disable an App Engine application, when you no longer want it to be visible.
    -Set up your lab environment


# Task 1: Initialize App Engine
1. Initialize your App Engine app with your project and choose its region using this command:
      gcloud app create --project=$DEVSHELL_PROJECT_ID
        # When prompted, select the region where you want your App Engine application located.

2. Clone the source code repository for a sample application in the hello_world directory:
         git clone https://github.com/GoogleCloudPlatform/python-docs-samples
3. To navigate to the source directory use the following command:
        cd python-docs-samples/appengine/standard_python3/hello_world

# Task 2: Run Hello World application 

1. Execute the following command to download and update the packages list.
        sudo apt-get update
2. Set up a virtual environment in which you will run your application.
         sudo apt-get install virtualenv
        virtualenv -p python3 venv
   ## If prompted [Y/n], press Y and then Enter.
3. Activate the virtual environment.
      source venv/bin/activate

4. Navigate to your project directory and install dependencies.

    pip install  -r requirements.txt

5. To Run the application:

    python main.py

    ## Please ignore the warning if any.

# Task 3: Deploy and run Hello World on App Engine

1. Navigate to the source directory:

        cd ~/python-docs-samples/appengine/standard_python3/hello_world

2. Deploy your Hello World application.

    gcloud app deploy

   ## If prompted "Do you want to continue (Y/n)?", press Y and then Enter.

3.  Launch your browser to view the app at http://YOUR_PROJECT_ID.appspot.com

    gcloud app browse

   ## Copy and paste the URL into a new browser window to view the results.


# Task 4: Disable the application

  ## The easiest way to disable application in App Engine is to use
           gcloud app versions stop
           ### or you can either follow the following tasks below.
    ## App Engine offers no option to Undeploy an application. After an application is deployed, it remains deployed, However, you can disable the application, which causes it to no longer be accessible to users. To do this you have to navigate to the cloud shell and then disable the application.
 
            gcloud app open-console

    ## a link will appear and use it to navigate to the app engine settings and disable the application

# Congratulations!
 You created your first application using App Engine!
