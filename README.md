## <h1>Building a Data Warehouse with Redshift
##### <h2>Introduction
A music streaming startup, Sparkify, has grown their user base and song database and want to move their processes and data onto the cloud. Their data resides in S3, in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

As their data engineer, you are tasked with building an ETL pipeline that extracts their data from S3, stages them in Redshift, and transforms data into a set of dimensional tables for their analytics team to continue finding insights in what songs their users are listening to. You'll be able to test your database and ETL pipeline by running queries given to you by the analytics team from Sparkify and compare your results with their expected results.
    

##### <h3>Description
Sparkify is a facing lot of problems querying its own data stored in json. They require to query and do lots of analytics and also their analytics drive their data science team as well. So, inorder to make things easy for them we are building an etl pipeline here which consumer json data store in s3 and store them as staging tables in redshift and later on creating facts and dimension tables out of the staging tables and inserting data. Facts and dimensional tables reside in redshift which uses columnar storage which increases our querying capability providing quick results.

##### <h3>Datasets
###### <h4>Log Dataset
{"artist":"Pavement", "auth":"Logged In", "firstName":"Sylvie", "gender", "F", "itemInSession":0, "lastName":"Cruz", "length":99.16036, "level":"free", "location":"Klamath Falls, OR", "method":"PUT", "page":"NextSong", "registration":"1.541078e+12", "sessionId":345, "song":"Mercy:The Laundromat", "status":200, "ts":1541990258796, "userAgent":"Mozilla/5.0(Macintosh; Intel Mac OS X 10_9_4...)", "userId":10}

###### <h4>Song Dataset
{"num_songs": 1, "artist_id": "ARJIE2Y1187B994AB7", "artist_latitude": null, "artist_longitude": null, "artist_location": "", "artist_name": "Line Renaud", "song_id": "SOUPIRU12A6D4FA1E1", "title": "Der Kleine Dompfaff", "duration": 152.92036, "year": 0}

##### <h3>Schema for fact table and dimensional tables
###### <h4>Fact table : songplays
songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent

##### <h3>Dimensional tables : users, songs, artists, time
users - user_id, first_name, last_name, gender, level songs - song_id, title, artist_id, year, duration artists - artist_id, name, location, latitude, longitude time - start_time, hour, day, week, month, year, weekday

##### <h3>Schema for staging tables : stagingevents, stagingsongs
stagingevents - event_id, artist, auth, firstName, gender, itemInSession, lastName, length, level, location, method, page, registration, sessionId, song, status, ts, userAgent, userId

stagingsongs - num_songs, artist_id, artist_latitude, artist_longitude, artist_location, artist_name, song_id, title, duration, year

##### <h3> Steps to run this the project
    1- Fill configuration file dwh.cfg with the information such [Access key ID - Secret access key] from credential csv file you downloaded when you create the IAM user.
    2- Open redshift service from AWS consol click on your cluster and fill the information for your cluster in dwh.cfg file
    3- Fill IRN [IAM_ROLE] in the file , you can git it from the exercises file from lesson 3 
    4- You should careful when you fill these information
    5- Open new Terminal and Excute this command 'python3 create_tables.py'
    6- This python file to drop and create tables 
    7- Then ,Run etl.py  for creating the etl pipeline to insert data into the created tables.