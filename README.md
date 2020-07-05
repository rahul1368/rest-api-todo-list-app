## REST API Tutorial for todo list app



## Introduction


**Todo-list-app is an application that allows a user to manage a list of tasks to do. It performs adding, updating, deleting and toggling state of each task. It has minimalistic design and basic functionality.**


App is a kind of model showing how to implement MVC approach in JavaScript. Model Controller, View (MVC) methodology separates data logic (model) from display functionality (View) and manages them using separate entities (Controller).


**So in this tutorial we will learn how to set up rest api endpoints for todo-list.**



## Prerequisites


*[Node.js (LTS)](https://nodejs.org/en/download/)*
*[MySQL( on Mac)] (https://tableplus.com/blog/2018/11/how-to-download-mysql-mac.html)*
*[MySQL WorkBench] (http://www.ccs.neu.edu/home/kathleen/classes/cs3200/MySQLWorkbenchMAC10.pdf)*
*[Code Editor of your Choice ( I will use vs code throughout the tutorial)](https://code.visualstudio.com/)*
*[Postman (For testing our api endpoints)](https://www.postman.com/downloads/)*




## Module Categorization

**We have divided our project’s backend structure into two modules i.e user and todos.**



**User Module:** This module will contain all api endpoints related to user



**API endpoints for User Module:**
    
* **/api/user/register:** To registering a user (method: POST)*
* **/api/user :** To fetching all users (method : GET)*
* **/api/user/login :** To logging a user (method : POST)*
* **/api/user/update :** To updating a user by user_id ( method : PATCH)*
* **/api/user/delete :** To deleting a user ( method: DELETE)*

**Todos Module:** This module will contain all api endpoints related to todos

**API endpoints for Todos Module:**

* **/api/todos/create:** To creating a new todo or task for a user ( method : POST)* 
* **/api/todos :** To fetching all todos or tasks for a user (method : GET)*
* **/api/todos/:task_id :** To fetching a particular todo or task for a user (method : GET)*
* **/api/todos/update :** To updating a todo or task by task_id for a user ( method : POST)*
* **/api/todos/delete/:task_id :** To deleting a todo or task for a user ( method: DELETE)*
* **/api/todos/delete :** To deleting al todo or task for a user ( method: DELETE)*



**Together all api endpoints will cover CRUD ( Create,Retrieve,Update & Delete ) operations.**

**Note:**  All api endpoints are private i.e users should be logged in( authenticated ) & must have token ( authorized ) to access them.We will use [jwt(jsonwebtoken)](https://jwt.io/introduction/) to secure api endpoints.

## Database & Schema

**For this tutorial , we will use mysql as a database.**

**Schema:**  According to our project requirements ,we have two tables(relations or entities) i.e users and tasks.

**users**( user_id( primary key ) , user_firstname, user_surname, user_email, user_password, user_registered)

**tasks**( task_id( primary key ), user_id(foreign key) , task_name , task_priority, task_status, task_color, task_description, task_date)

```
    CREATE DATABASE todo;

    USE todo;

    CREATE TABLE IF NOT EXISTS `users` (
    `user_id` bigint(20) unsigned NOT NULL auto_increment,
    `user_password` varchar(64) NOT NULL,
    `user_firstname` varchar(50) NOT NULL,
    `user_surname` varchar(50) NOT NULL,
    `user_email` varchar(100) NOT NULL,
    `user_registered` datetime NOT NULL default CURRENT_TIMESTAMP,  
    PRIMARY KEY (`user_id`),
    INDEX `idx_user_key` (`user_email`)
    ) DEFAULT CHARSET=utf8 AUTO_INCREMENT=1;

    CREATE TABLE IF NOT EXISTS `tasks` (
    `task_id` bigint(20) unsigned NOT NULL auto_increment,
    `user_id` bigint(20) NOT NULL REFERENCES `users`(`user_id`),
    `task_name` varchar(60) NOT NULL,
    `task_priority` tinyint(2) NOT NULL default '2',
    `task_status` tinyint(1) NOT NULL default '0',
    `task_color` varchar(7) NOT NULL default '#ffffff',
    `task_description` varchar(150) NULL,
    `task_date` datetime NOT NULL default CURRENT_TIMESTAMP,  
    PRIMARY KEY (`task_id`),
    INDEX `idx_task_key` (`task_name`,`task_id`)
    ) DEFAULT CHARSET=utf8 AUTO_INCREMENT=1;
```

## Installation
    
```
    # Clone repository into local
    
    git clone https://github.com/rahul1368/rest-api-todo-list-app.git todo-list

    # Go to todo-list directory
    
    cd todo-list 

    # Install devDependencies
    
    npm i  or npm install 

    # Start the server
    
    npm run start

```




