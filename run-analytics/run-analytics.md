# Run Analytics - Create Dashboards

## Introduction

In this lab, you will use a DVA file to get started with HR Departmental analytics in Oracle Analytics Cloud.

## Objectives

- Create connection to ADW  
- Upload DVA file and refresh the data flowing through the connection
- View analysis.

## Prerequisites

- Autonomous Data Warehouse (ADW) and Oracle Analytics Cloud (OAC) instances.
- Access to the files needed to recreate this demo. 
    - [AttritionPrediction.csv](https://objectstorage.us-ashburn-1.oraclecloud.com/p/fp-wLXQ7mf0Q5Dtae0hH9o1VABJujAfRI2UOVs4dzsU/n/oradbclouducm/b/bucket-20200907-1650/o/AttritionPrediction.csv)
    - [HumanResources.dva](https://objectstorage.us-ashburn-1.oraclecloud.com/p/0VqpqURMs3ARIovzyCfR369sv5qqvVxMkmGbag8-wWA/n/oradbclouducm/b/bucket-20200907-1650/o/HumanResource.dva)
    - [hr.sql](https://objectstorage.us-ashburn-1.oraclecloud.com/p/k_O2qXLAvew-YfooziwLpiHgHau_1HQO6438oc20m2LM3WwhH1gGQElUZTs8bBjZ/n/oradbclouducm/b/bucket-20200907-1650/o/hr.sql)

Note: Please download the files above before continuing.

### STEP 1: Installing HR Schema on Autonomous Database

- Use SQL Developer to connect to your database as the ADMIN user. The steps to do so can be found [here](https://docs.oracle.com/en/cloud/paas/autonomous-data-warehouse-cloud/user/connect-sql-dev182.html#GUID-14217939-3E8F-4782-BFF2-021199A908FD).

- Run the following code to create the HR user. You should replace MYpassword12 in the statement below with a password of your choosing.

````
CREATE USER HR IDENTIFIED BY MYpassword12;

GRANT DWROLE TO HR;

ALTER USER HR QUOTA UNLIMITED ON DATA;

````

- Now go ahead and log in as the HR user, then run the hr.sql script to install the HR schema. 

- The following tables should be visible: EMPLOYEES, LOCATIONS, JOBS, COUNTRIES, DEPARTMENTS, REGIONS, JOB_HISTORY

    ![](./images/1.png " ")
    
### STEP 2: Setting up the Human Resource Analytics Project in OAC

- Login to your analytics cloud instance. The URL can be found on the page of the instance. Refer to the previous lab for instructions on how to get to your analytics cloud instance.

    ![](./images/2.png " ")

- Click on the ellipses menu on the right-side, select **Import Project/Flow**. Then click on **Select File** and choose the HumanResources.dva file.

    ![](./images/3.png " ")
    ![](./images/4.png " ")

-  Import the file into OAC by clicking on **Import**. The password is **Admin123**. Hit OK to close the dialog. 

    ![](./images/5.png " ")
    ![](./images/6.png " ")

- Click on the navigation menu icon in the top left. Go to **Data** and open the **Connections** tab. You should see a connection named 'adw_hr'. 

    ![](./images/7.png " ")
    ![](./images/7a.png " ")

- Click on the ellipses menu on the extreme right of the connection’s name and select inspect.

     ![](./images/7b.png " ")

- Click on the **Select** button in front of Client Credentials and select the wallet to your ADW instance. Let the username be **ADMIN** and provide the database password. Click **Save**.

    ![](./images/8.png " ")

- We will now refresh our data sets to utilize our connection. Select the **Data Sets** tab and you will see all our tables appear below. Go ahead and reload each data set by clicking on the ellipses menu to the right of the data set's name and selecting **Reload Data**.

    ![](./images/9.png " ")

- Now proceed to the hamburger menu and select **Catalog** and open your project. The visualizations should load, but click **Refresh Data** if needed to refresh the visuals.

    ![](./images/10.png " ")
    ![](./images/10a.png " ")

### STEP 3: Uploading a file to the Datawarehouse using OAC

- Return to the home page. Click on the **Create** button and then select **Data Flow**.

    ![](./images/11.png " ")

- Select the **Create Data Set**, choose the **Click to Browse** option and select the AttritionPrediction.csv file. 

    ![](./images/12.png " ")
    ![](./images/13.png " ")

**Note:** You may drag and drop the file instead.

- Once the file is uploaded, select **Add**.
    ![](./images/14.png " ")

- Next, drag the **Save Data Set** option from the **Data Flow Steps** on the left, and move it right next to the Attrition Prediction data set in the panel at the top. Provide a name to the Data Set. In the **Save Data To** drop down, select **Database Connection**. 

    ![](./images/15.png " ")

- Click on **Select connection** and choose the adw_hr connection. Thereafter, also give a name that would be used for the table in the database.

    ![](./images/16.png " ")

- Hit the **Run Data Flow** button at the top. You will be prompted to save the data flow. Give it a name and click on **Save & Run**.

    ![](./images/17.png " ")

The data flow should run and upon successful execution you should be able to see the two data sets under the **Data** menu item.

![](./images/18.png " ")

### STEP 4: Using Attrition Data set in the Human Resource project

- Open the Human Resource project. From the data panel, click on the 'plus' sign and select **Add Data Set**.

    ![](./images/19.png " ")

- Select the **AttritionPrediction** data set that is stored in the database.    
    
    ![](./images/20.png " ")

- Click on the '+' sign next to the canvas names at the bottom of the screen to add a new canvas. 

    ![](./images/21.png " ")

- Right click on the name of the new canvas and choose **Rename**. Give the canvas a meaning full name.

    ![](./images/22.png " ")

- Now drag the **Employee Count** data item under Attrtion Prediction to this canvas to get you first visualisation. 

    ![](./images/23.png " ")

We will now leave it upto your imagination to analyse the data sets that have been provided to you.
