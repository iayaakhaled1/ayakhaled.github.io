### Part 1: To set up a Python virtual environment and install Airflow on Ubuntu, you can follow these step-by-step instructions:
1) set up with Windows System for Linux.
   - Click on the start menu, and search for Windows features.
   - Now, you'll see an option called Turn Windows features on or off in the control panel -->  you should find an option for Windows Subsystem for Linux --> check that option
   - This will set up WSL on your Windows machine. Click on the OK button.
   - Once this is complete, you'll need to restart your machine for this feature to take effect.
   ![image](https://github.com/iayaakhaled1/airflow/assets/145045777/f69b3ff0-b6df-4bde-b469-e1f61ac754ad)
2) Install Ubuntu
    - Once the restart is complete, come back to the Start menu, and search for the Microsoft Store --> Search for the Ubuntu distribution.
    - Install Ubuntu to work the Linux virtual machine using WSL.
    - Click on the get button here to get the Ubuntu terminal environment.
    - Once the installation is complete, click on Open. And in a few minutes, you'll see a Linux terminal that you can use.
------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Part 2: Install Airflow on Ubuntu system
1) Open a terminal on your Ubuntu system.
  - You need to code sudo apt update and upgrade , so that all of the components of your Ubuntu distribution have been updated.
```
sudo apt update
sudo apt upgrate
```
2) Next thing is to install plp --> Python package manager. Once plp is available on your machine, you can use this to install the Python libraries that you need.
```
sudo apt  install python3-pip
```
  ------------------------------------------------------------------------------------------
3) Install the virtual environment package by running the following command
```
sudo apt-get install python3-venv
```
------------------------------------------------------------------------------------------
4) Create a new directory for your Airflow project and navigate to it:
```
mkdir airflow-project
cd airflow-project
```
------------------------------------------------------------------------------------------
- Now, you are inside the virtual environment. You should see (venv) at the beginning of your terminal prompt.
5) Activate the virtual environment by running the activation script:
```
source venv/bin/activate
```
- Upgrade pip to the latest version (optional)
```
pip install --upgrade pip
```
------------------------------------------------------------------------------------------
6) Install Airflow and its dependencies using pip: [apache-airflow-docs](https://airflow.apache.org/docs/apache-airflow/stable/installation/installing-from-pypi.html)
```
pip install "apache-airflow[celery]==2.8.0" --constraint "https://raw.githubusercontent.com/apache/airflow/constraints-2.8.0/constraints-3.8.txt"
```
- This message indicates that Apache Airflow, along with all of its dependencies, has been successfully installed.
   ![image](https://github.com/iayaakhaled1/airflow/assets/145045777/ede6fe46-57d6-45f9-ac30-e54661434e81)
- Once the Airflow installation is complete all you need to do is run Airflow version.
```
airflow version
```
------------------------------------------------------------------------------------------
7) All tasks that you can perform with the Airflow UI you can perform on the command line with the Airflow command.
   -  Now, Airflow info will give you information about your current Airflow installation.
```
airflow info
```
- Apache Airflow's configuration settings are organized into distinct sections, with each section title highlighted in green for easy navigation. 
- These settings are designed to be customizable, allowing you to fine-tune Airflow to meet your specific needs.
![image](https://github.com/iayaakhaled1/airflow/assets/145045777/d7868bad-a25e-44cb-821c-a6533b000869)
------------------------------------------------------------------------------------------
8) To check the content of airflow config files
```
ls -l
```
![image](https://github.com/iayaakhaled1/airflow/assets/145045777/4e853b28-6b24-4170-87e6-cd8e2407ca31)

------------------------------------------------------------------------------------------
 9) You can interact with this config file from the UI but you can also call airflow config on the command line and interact with the config file.
```
airflow config get value webserver base_url
```
 -  airflow config get value webserver base_url will tell us that the web server will run on localhost 8080.
 ------------------------------------------------------------------------------------------
10) Airflow requires a database.
- if you're just experimenting and working with Airflow, you can stick with the default SQLite database.
- In a production environment, you need to configure PostgreSQL or some other production database.
```
airflow db init
```
------------------------------------------------------------------------------------------
### Part 3: Web Authentication
- By default, Airflow requires users to specify a password prior to login. You can use the following CLI commands to create an account:
- create an admin user--> [airflow_docs](https://airflow.apache.org/docs/apache-airflow/stable/security/webserver.html)
```
airflow users create \
    --username admin \
    --firstname Peter \
    --lastname Parker \
    --role Admin \
    --email user_name@domain
```
- a new user will be created
- use this user to log in to our Airflow UI
------------------------------------------------------------------------------------------
### Bring up the Airflow services to run Airflow
- Start the Airflow web server and scheduler:
  -  The Airflow web server provides the user interface for managing and monitoring workflows, while the scheduler is responsible for executing tasks based on the defined workflows.
  - Running Airflow Scheduler will bring up the scheduler running on your local machine.
```
airflow scheduler
```
  - Now, along with the scheduler, you need to run a web server, open up a new tab on the terminal , make sure you're within the Airflow environment (you need to active the virtual environment)
```
airflow webserver
```
- The web server will start on a specified host and port, allowing you to access the Airflow UI in a web browser.
- At this point, Airflow should be up and running successfully on your local machine.
![image](https://github.com/iayaakhaled1/airflow/assets/145045777/9d2ae6d8-c9fe-40dd-b8dc-aab453333b5c)
------------------------------------------------------------------------------------------
###  Access the Airflow web interface
- The Airflow webserver typically runs on localhost and listens on a specific port. By default, the port used is 8080.
- Therefore, the URL to access the Airflow web interface on localhost would be http://localhost:8080.
- To access the Airflow web interface from your local machine, you can open a web browser and enter http://localhost:8080 in the address bar. 
- If the webserver is running and reachable, you should see the Airflow UI, where you can manage your workflows and perform other Airflow-related tasks.
![image](https://github.com/iayaakhaled1/airflow/assets/145045777/965d78e8-a5d8-452d-a38d-8ba82093c640)
------------------------------------------------------------------------------------------
### Define and manage workflows:
- With Airflow up and running, you can define your workflows using Python code or the Airflow UI.
- Workflows in Airflow are represented as Directed Acyclic Graphs (DAGs) and consist of tasks that are executed based on dependencies and schedules.
- You can create your own DAGs by defining Python scripts in the specified dags_folder in the Airflow configuration. Alternatively, you can use the Airflow UI to create and manage DAGs interactively.
- Monitor and manage workflows: Once your workflows are running, you can monitor their progress and manage their execution.
- The Airflow UI provides a dashboard where you can view the status of your workflows, inspect task logs, and manually trigger or pause workflows.
