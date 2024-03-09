# Task Manager Application 


## What is this Application?
  
  This is a Flask based Task management system allowing users to schedule, edit, and prioritize events. Users can log in, add, and track tasks, receive email alerts, and customize their task management preferences. The application includes features for user authentication, dynamic scheduling, and personalized email notifications for improved productivity. 
  
You may access the application [here](https://task-manager-application-37yuo72rz-vinay-rohit-reddy-s-projects.vercel.app/).


## Introduction
  - This Flask-based Task Manager application allows users to perform various task-related operations. 
  - Users can register, log in, add, edit, delete, and mark tasks as completed.
  - It also sends reminders for the overdue tasks by end of the day.

## Features
  - **User Authentication:** Users can sign up and log in securely.
  - **Task Management:** Add, edit, delete, and mark tasks as completed.
  - **Email Reminders:** Sends reminders for overdue tasks via email.
  - **Responsive UI:** User-friendly interface for managing tasks.
  - **Database:** PostgreSQL database used to store user data and task details.

## Installation
### 1. Clone the repository:
    git clone https://github.com/rohitreddy192/Task-Manager-Application.git
### 2. Navigate to the project directory:
    cd Daily_Task_Scheduler
### 3. Install Dependencies:
    pip install -r requirements.txt
    
## Local Usage
### 1. Run Application:
     python app.py
### 2. Access the Application:
    - Open a web browser and go to http://localhost:5000 to access the Task Manager application.
### 3. Functionalities:
    - Register or log in to manage tasks.
    - Add, edit, delete tasks, and mark them as completed.
    - Receive email reminders for overdue tasks.
    
## Technologies Used
  - Flask
  - PostgreSQL
  - HTML/CSS
  - JavaScript
  - Python 3.x

## File Structure
```bash
├── app.py                  # Main Flask application file.
├── requirements.txt        # Contains all requirements necessary for the application.
├── runtime.txt             # Defines the runtime used for the application.
├── vercel.json             # Contains the deployment information required to host and run the application.
└── templates/
    ├── base.html       
    ├── add.html           
    ├── completed_tasks.html           
    ├── edit_task.html
    ├── email_alert.html       
    ├── email_template.html           
    ├── forgot_password.html           
    ├── index.html
    ├── login.html       
    ├── profile.html           
    ├── reset_password.html           
    ├── signup.html
```

## Data Models

### User

  The `User` class represents the user entity in the application, encapsulating the following attributes:

  - **id**: Unique identifier for each user (Primary Key).
  - **name**: User's name (String, 80 characters, unique, not nullable).
  - **password**: User's password (String, 255 characters, not nullable).
  - **email**: User's email address (String, 120 characters, unique, not nullable).
  - **email_alert**: Boolean indicating whether email alerts are enabled (Default: False).

### Event

  The `Event` class represents scheduled events associated with a user, featuring the following attributes:

  - **id**: Unique identifier for each event (Primary Key).
  - **task_name**: Name of the task or event (String, not nullable).
  - **date**: Date of the event (Date, not nullable).
  - **time**: Time of the event (Time, not nullable).
  - **duration**: Duration of the event in minutes (Integer, not nullable).  
  - **notes**: Additional notes for the event (Text).
  - **completed**: Integer indicating completion status (Default: 0).
  - **priority**: Integer indicating priority level (Default: 5).
  - **user_id**: Foreign key linking the event to a specific user.

  These data models provide a structured representation of user information and scheduled events within the application. The `User` model captures essential user details, while the `Event` model allows for the management of scheduled tasks associated with a user. Adjustments can be made based on specific project requirements and database design considerations.

## Forms

  In this Flask application, various forms are used to facilitate user interactions. The forms are created using the Flask-WTF extension, providing a convenient way to handle form data validation and submission.

### LoginForm

  The `LoginForm` allows users to log in by providing their username and password.

  Fields:
  - **username**: String field for the username (required).
  - **password**: Password field for the user's password (required).

### RegistrationForm

  The `RegistrationForm` enables users to create a new account by providing a username, email, and password.

  Fields:
  - **username**: String field for the new username (required).
  - **email**: String field for the user's email address (required, must be a valid email).
  - **password**: Password field for the user's password (required).
  - **confirm_password**: Password field to confirm the entered password (required, must match the password).

### EventForm

  The `EventForm` is designed for users to submit details for scheduling events.

  Fields:
  - **task_name**: String field for the name of the task or event (required).
  - **date**: Date field for specifying the date of the event (required).
  - **time**: Time field for specifying the time of the event (required).
  - **duration**: Integer field for specifying the duration of the event in minutes (required).
  - **notes**: TextArea field for additional notes.
  - **completed**: Integer field (default: 0) for completion status (assuming it's a checkbox or similar).
  - **priority**: Integer field (default: 5) for indicating the priority level of the event.

### EmailForm

  The `EmailForm` is used for enabling or disabling email alerts for a user.

  Fields:
  - **email_alert**: Boolean field for enabling or disabling email alerts (required).

### ForgotPasswordForm

  The `ForgotPasswordForm` assists users in resetting their passwords by providing their username and email.

  Fields:
  - **username**: String field for the username (required).
  - **email**: String field for the user's email address (required, must be a valid email).

  These forms enhance the user experience by providing structured and validated input for various functionalities within the application.


## Routes

### Authentication

#### Login Route

  - **Route:** `/login`
  - **Method:** GET, POST
  - **Description:** Enables users to log in, validates entered credentials, and redirects to the home page upon successful login.

#### Logout Route

  - **Route:** `/logout`
  - **Method:** GET
  - **Description:** Logs out the current user and redirects to the login page.

#### Signup Route

  - **Route:** `/signup`
  - **Method:** GET, POST
  - **Description:** Allows users to create a new account, validates user input, and redirects to the login page upon successful registration.

#### Forgot Password Route
  
  - **Route:** `/forgot_password`
  - **Method:** GET, POST
  - **Description:** Initiates the password reset process by providing the username and email, then sends a password reset email.

### Task Management

#### Home Page

  - **Route:** `/`
  - **Method:** GET, POST
  - **Description:** The home page/dashboard displays tasks scheduled for the current user, allowing users to add new tasks and view upcoming events.

#### Add Event Route

  - **Route:** `/add_event`
  - **Method:** GET, POST
  - **Description:** Allows users to add a new task/event, validates user input, and redirects to the home page upon successful addition.

#### Get Task Details Route

  - **Route:** `/get_task_details/<int:task_id>`
  - **Method:** GET
  - **Description:** Retrieves details of a specific task identified by `task_id` and returns the information as JSON.

#### Edit Task Route

  - **Route:** `/edit_task/<int:task_id>`
  - **Method:** GET, POST
  - **Description:** Enables users to edit an existing task, displaying the current task details and updating the task upon form submission.

#### Mark Completed Route

  - **Route:** `/mark_completed/<int:task_id>`
  - **Method:** POST
  - **Description:** Marks a task as completed based on the `task_id` and updates the database accordingly.

#### Completed Tasks Route

  - **Route:** `/completed_tasks`
  - **Method:** GET, POST
  - **Description:** Displays a list of completed tasks for the current user.

#### Prioritize Schedule Route

  - **Route:** `/prioritize_schedule`
  - **Method:** GET, POST
  - **Description:** Displays the prioritization feature for scheduling tasks.

#### Prioritize Task Route

  - **Route:** `/prioritize_task/<int:task_id>`
  - **Method:** POST
  - **Description:** Allows users to prioritize a specific task by updating its priority level.

#### Email Alert Settings Route
  
  - **Route:** `/email_alert_settings`
  - **Method:** GET, POST
  - **Description:** Displays the email alert settings for the user.

#### Update Email Alert Route
  
  - **Route:** `/update_email_alert`
  - **Method:** POST
  - **Description:** Updates the email alert settings for the current user based on the form input.

#### Add Task Route
  
  - **Route:** `/add_task`
  - **Method:** GET, POST
  - **Description:** Redirects to the `/add_event` route for adding a new task.

#### Delete Task Route

  - **Route:** `/delete_task/<int:task_id>`
  - **Method:** GET, POST
  - **Description:** Deletes a task identified by `task_id` from the user's schedule.

### Email Alerts and Notifications

#### Scheduled Task Route

  - **Route:** `/scheduled-task`
  - **Method:** GET
  - **Description:** Sends overdue email alerts for tasks scheduled for the current user. Runs a scheduled task to check and send alerts for overdue tasks.

  These routes handle various aspects of user authentication, task management, and email alerts within the application. Adjustments can be made based on specific project requirements and functionality.

## Future Scope & Reference
  1. This can be further added with many features by integrating with the calendar directly on the system so that we can get a calendar remainder always..
  2. Implementing an AI generated Task Scheduling Algorithm which can schedule the tasks by user priority and User can select from the options or he may do it manually..

## Contributions
  Contributions are welcome! If you'd like to contribute to this project, feel free to create issues or pull requests.
