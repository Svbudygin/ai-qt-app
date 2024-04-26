# Technical Specification for a Qt C++ Application

## General Description
Develop a Qt C++ application that provides user login/registration functionality, post creation and editing using Yandex GPT, and viewing the history of all posts. The application should ensure secure storage of user data through hashing, interact with the Yandex GPT external API for text generation, and use SQLite for storing posts and user data.

## Section 1: Login/Registration
### 1.1 Login:
- Upon launching the application, it checks for user data in the SQLite database.
- If user data is found, the application sends a request to the server to verify the correctness of the user information (login, hashed password, and token).
- If no user data is found in the database or if it is incorrect, the login screen opens.
- The user enters their credentials (username and password) to log in.
- Upon successful login, the user is provided with their data and token for subsequent use.

### 1.2 Registration of a New Account:
- If no user data or incorrect data is found, the registration screen opens.
- The user fills out the registration form, including the following fields:
    - Email
    - Password
    - First Name
    - Last Name
    - Telegram Channel ID (optional)
- After filling out the form, the user sends a request to the server to register a new account.
- The server checks the uniqueness of the email and hashes the password before saving it to the database.
- After successful registration, the user is provided with their data and token for subsequent use.

## Section 2: Main Page (Post Editor using Yandex GPT)
### 2.1 Post Editing:
- Upon successful login, the main page opens, where the editor for creating and editing posts is located.
- The editor provides the user with a field to enter the post description.
- After entering the post description, the user can click the "Generate Post" button to have Yandex GPT generate the post text based on the entered description. After text generation, it replaces the entered description.
- The user can edit the generated post text in the same window.
- If necessary, the user can click the "Back" button to re-enter the post description and repeat the generation process.
- The user also has the option to click the "Regenerate" button to regenerate the post text using Yandex GPT.
- Before submitting the post, the user can preview it by clicking the "Preview Post" button. This opens a preview window where the user can see how the post will look with text and (if available) an image.

### 2.2 Creating a Post with an Image:
- After editing the post text, the user can click the "Next" button to proceed to create a post with an image.
- On the next screen, the user is provided with the option to choose how to create a post with an image:
    - Ability to enter an image description in a text field.
    - Ability to add their own image by clicking the "Add Your Own Photo" button.
- After entering the description and, if necessary, adding their own image, the user can click the "Send" button to create a post with text and an image.

## Section 3: History of All Posts:
- The user should have access to the history of all posts they have created.
- Posts should be saved in the SQLite database with a timestamp.
- The user should be able to view and edit previously created posts.

## Section 4: SQLite Database
### 4.1 Database Structure:
- The application uses SQLite to store user data and system variables.
- The database contains two tables: "Users" and "SystemVariables".

### 4.2 "Users" Table:
- This table contains information about registered users.
- Table Structure:
    - id (INTEGER, PRIMARY KEY): unique user identifier.
    - login (TEXT, UNIQUE): user login.
    - password_hash (TEXT): hashed user password.
    - email (TEXT, UNIQUE): user email address.
    - telegram_chat_id (TEXT, UNIQUE): user's Telegram chat ID (optional).

### 4.3 "SystemVariables" Table:
- This table contains system variables such as API tokens and other application settings.
- Table Structure:
    - id (INTEGER, PRIMARY KEY): unique record identifier.
    - name (TEXT, UNIQUE): variable name.
    - value (TEXT): variable value.

### 4.4 Using System Variables:
- The API token (e.g., for Yandex GPT) is stored in the "SystemVariables" table under a specific name (e.g., "api_token").
- SQL queries to the "SystemVariables" table are used to update or retrieve the token.

### 4.5 Data Security:
- To ensure the security of user passwords, they are hashed before being saved to the database.
- To protect against potential security threats, user data (login, password, email) should be stored in encrypted form.
- Use parameterized SQL queries to prevent SQL injection attacks.

## Technology Stack:
- Qt C++ for developing the graphical interface and application logic.
- Hashing libraries for securely storing user passwords.
- HTTP requests for interacting with the Yandex GPT API for text generation.
- SQLite database for storing user and post information.

## Upon Completion of Development:
- Ensure testing of the application for compliance with functional requirements and security.
- Provide error and exception handling to improve application reliability.
- Verify compliance with data protection requirements when collecting, storing, and processing user information.
