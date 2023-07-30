# MyFirstAPI
First JS api with MySQL and docker

Objective Create a JSON API Server that will receive GET and POST requests from any external client. The API server will connect with any SQL database (of your choice) and the server will be able to write the data received from APIs to the server and return the result based on the query. The read query will be able to support filters as well as defined by the data model. The entire stack (API Server & database) should be containerized in a docker container and the ecosystem should be able to run with a simple docker-compose up command.

##Specification
Data Model ::
1. Teacher 
a. teacher_id
b. name
c. is_active
d. designation

2. Course
a. course_id
b. course_mentor
c. name
d. start_date
e. end_date
f. description
g. is_active


##API Specification 
1. GET - /teacher/{id} - Get a specific teacher record by ID.
a. Example Request: /teacher/1 Example Response: {
“teacher_id”:1, “name”:”Jason”, “is_active:true,“designation”:”Professor” }
2. GET - /teacher?<field=value> - Get a list of teachers based on filters.
a. Example Request: /teacher?name=Jason&is_active=true
Example Response:
[
{
“teacher_id”:1,
“name”:”Jason”,
“is_active:true,
“designation”:”Professor”
},{
“teacher_id”:5,
“name”:”Jason”,
“is_active:true,
“designation”:”Associate Professor”
}
]
4. Post - /teacher - Create a new teacher record using the JSON payload
a. Example request: - /teacher
{
“teacher_id”:1,
“name”:”Jason”,
“is_active:true,
“designation”:”Professor”
}
Example response:
{
“teacher_id”:1,
“name”:”Jason”,
“is_active:true,
“designation”:”Professor”
}
5. GET - /course?<field=value> - Get a list of courses based on filters.
a.
Example Request: - /course/
Example Response:
[{
“course_id”:1,
“Course_mentor”:{
“teacher_id”:6,
“name”:”John”,
“Is_active”:true,“designation”:”Assistant Professor”
},
“name”:”Introduction to Devops”,
“start_date”:”2024-01-01”,
“end_date”:”2024-02-02”
“description”:”Basic concepts of DevOps”,
“is_active”:true
}]
6. POST - /course - create a new course using the JSON payload
a. Example Request: - /course/
{
“course_id”:1,
“course_mentor”:6,
“name”:”Introduction to Devops”,
“start_date”:”2024-01-01”,
“end_date”:”2024-02-02”
“description”:”Basic concepts of DevOps”,
“is_active”:true
}
Example Response:
{
“course_id”:1,
“Course_mentor”:{
“Teacher_id”:6,
“name”:”John”,
“Is_active”:true,
“designation”:”Assistant Professor”
},
“name”:”Introduction to Devops”,
“start_date”:”2024-01-01”,
“end_date”:”2024-02-02”
“description”:”Basic concepts of DevOps”,
“is_active”:true
}
7. GET - /course/{id}
a. Example Request: - /courses/1
Example Response: {
“course_id”:1,
“Course_mentor”:{
“Teacher_id”:6,
“name”:”John”,
“Is_active”:true,
“designation”:”Assistant Professor”
},“name”:”Introduction to Devops”,
“start_date”:”2024-01-01”,
“end_date”:”2024-02-02”
“description”:”Basic concepts of DevOps”,
“is_active”:true
}
Containerisation
Api Server :
1. Listening Port : 8080
Database:
1. port : 5000
Deliverables
Code
Your deliverable should contain a zip file containing everything that is needed for the application
& database to run in a containerized environment. The zip file should have the following:
● src - Top level folder at the root of the zip that should contain everything else within.
● setup.sh - A bash script that does the following
○ Runs the Docker files to build your api server & database
■ API Server docker container image should be named
assignment-api-server-image
■ Database docker container image should be named
assignment-database-image
● docker-compose.yaml - Docker compose file to startup your containers.
○ Api Server should be called : assignment-api-server
○ Database should be called : assignment-database
Documentation
Provide a report documenting the work & research you undertook to complete the assignment.
Your report must contain a section for each of the specification headers. Proof of work must
contain reference links to sources used, an explanation of your take on the technology used &
screenshots of the component running. The screenshots should be accompanied with
description.Sample Test cases
Test case 1 :
Command:
curl --location --request POST 'http://localhost:8080/teacher' \
--header 'accept: application/json' \
--header 'Content-Type: application/json' \
--data '{
"teacher_id":1,
"name":"Jason",
"is_active":true,
"designation":"Professor"
}'
Output:
Response Code: 200
Json:
{
"teacher_id":1,
"name":"Jason",
"is_active":true,
"designation":"Professor"
}
Test case 2 :
Command:
curl --location --request GET 'http://localhost:8080/teacher/1' \
--header 'accept: application/json' \
--header 'Content-Type: application/json'
Output:
Response Code: 200
Json:
{
"teacher_id":1,"name":"Jason", "is_active":true, "designation":"Professor"
}
Test case 3: Command: curl --location 'http://localhost:8080/teacher?name=Jason&is_active=true' \ --header 'accept: application/json' \ --header 'Content-Type: application/json' Output:
Response Code: 200 Json:
[ {
"teacher_id":1, "name":"Jason", "is_active":true, "designation":"Professor" }
