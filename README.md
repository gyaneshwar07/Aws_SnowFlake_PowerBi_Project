AWS + Snowflake + Power BI Project

This project shows how I connected AWS S3, Snowflake, and Power BI to build a complete data pipeline.
I uploaded data in AWS, loaded it into Snowflake, transformed it, and finally created visualizations in Power BI.

📌 Project Workflow (Step-by-Step)
1️⃣ Create S3 Storage on AWS

I logged into AWS.

Created an S3 bucket.

Uploaded my dataset file into that S3 bucket.

2️⃣ Create IAM Role

Created a new IAM role in AWS.

Gave permissions to access S3 bucket.

This role is used later by Snowflake to read data.

3️⃣ Connect AWS with Snowflake

Opened Snowflake and created a new worksheet.

Created a Storage Integration Object in Snowflake.

This integration connects Snowflake with AWS using the IAM role.

code example - 
 CREATE OR REPLACE STORAGE INTEGRATION tableau_Integration
  TYPE = EXTERNAL_STAGE
  STORAGE_PROVIDER = 'S3'
  ENABLED = TRUE
  STORAGE_AWS_ROLE_ARN = 'arn:aws:iam::825765422200:role/tableau.role'
  STORAGE_ALLOWED_LOCATIONS = ('s3://tableau.project/')
  COMMENT = 'Optional Comment'


  //description Integration Object
  desc integration tableau_Integration;

  4️⃣ Load Data into Snowflake

Created a file format and stage.

Loaded data from S3 into Snowflake tables using:

code example - 

CREATE database PowerBI;

create schema PBI_Data;

create table PBI_Dataset (
Year int,	Location string,	Area	int,
Rainfall	float, Temperature	float, Soil_type string,
Irrigation	string, yeilds	int,Humidity	float,
Crops	string,price	int,Season string



);

select * from PBI_Dataset;

//drop database test;

create stage PowerBI.PBI_Data.pbi_stage
url = 's3://powerbi.project'
storage_integration = PBI_Integration

//desc stage s1

//drop stage s1;


copy into PBI_Dataset 
from @pbi_stage
file_format = (type=csv field_delimiter=',' skip_header=1 )
on_error = 'continue'

list @pbi_stage
5️⃣ Transform Data in Snowflake

Cleaned the data.

Used SQL queries to transform the data , adding columns.

Created a new final output table for Power BI.

6️⃣ Connect Snowflake to Power BI

Opened Power BI Desktop.

Selected Snowflake connector.
,

7️⃣ Data Visualization in Power BI

Created dashboards and visuals based on the Snowflake data.

Used charts, KPIs etc.

Focused on showing useful insights from the dataset.

📁 Technologies Used

AWS S3 (Storage)

AWS IAM (Role permissions)

Snowflake (Data warehouse)

SQL (Transformations)

Power BI (Dashboard and reporting)

📊 Final Output

Clean and structured dataset in Snowflake

Connected Live to Power BI

Interactive visual dashboard

⭐ What I Learned

How to integrate AWS S3 with Snowflake

How Snowflake manages roles, warehouses, and integrations

How to use Power BI with Snowflake

End-to-end data pipeline creation



<img width="809" height="622" alt="image" src="https://github.com/user-attachments/assets/aece0458-736c-4626-8372-b5be8af1970b" />
<img width="638" height="636" alt="image" src="https://github.com/user-attachments/assets/bbd94039-dfba-413a-bcd8-92f9622232bf" />
<img width="553" height="668" alt="image" src="https://github.com/user-attachments/assets/c8f21b2c-c98f-4491-9538-1ff581a6004c" />
<img width="800" height="500" alt="image" src="https://github.com/user-attachments/assets/83460027-99b5-41a3-b214-ce88eb99effb" />
<img width="1067" height="587" alt="image" src="https://github.com/user-attachments/assets/2aaaadf7-e8fe-473a-aeaf-c2b1514fdc39" />
<img width="1294" height="717" alt="image" src="https://github.com/user-attachments/assets/d70f9baa-a729-4b6b-98d4-2688eb2732aa" />
<img width="1288" height="709" alt="image" src="https://github.com/user-attachments/assets/44c60506-98e7-4ecd-9ca0-323112828769" />
<img width="1303" height="715" alt="image" src="https://github.com/user-attachments/assets/24de3aff-ddff-48d3-bcc1-93fafcc1e348" />






