# ✅ To-Do Application 
This project is a ToDo application built using React.js. Users can log in, view, and edit their ToDo lists. User authentication is handled using JWT tokens. Additionally, the application supports uploading images and files.

**Technologies Used:**
* React.js
* TypeScript 
* Node.js
* Express.js
* PostgreSQL
* JWT (JSON Web Token)
* SCSS
* Tailwind CSS
* Sequelize

# Frontend Setup
Clone the project to your local machine:

```bash
git clone https://github.com/senaoz/playable-to-do-app.git
cd todo-app
```

In the project directory, you can run the following commands to install dependencies and start the application:

```bash
npm install
npm start
```

Runs the app in the development mode. Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits. You will also see any lint errors in the console.

<hr />

## Interfaces

```typescript
interface Todo {
    id: string;
    title: string;
    description: string;
    image: string;
    status: boolean;
    dueDate: string;
    tags: string[];
}

interface User {
    email: string;
    password: string;
    first_name: string;
    last_name: string;
}

```

<hr />

# Backend Setup & API Endpoints

I implemented CRUD (Create, Read, Update, Delete) operations for a todo list using Express.js and Sequelize. These routes handle creating, reading, updating, and deleting items from a database.

Here's a breakdown of each route:

## To-Do Routes
### Create a new todo: `POST /api/todos`
-   Accepts a JSON object in the request body containing `title`, `description`, `status`, `due_date`, `userId`, `image`, and `tags`.
-   Creates a new todo item with the provided data and saves it to the database.
-   If successful, returns the created todo item as JSON.

### Get all todos: `GET /api/todos`
-   Retrieves all todo items from the database.
-   Returns an array of todo items as JSON.

### Get a todo by id: `GET /api/todos/:id`
-   Accepts the todo item's id as a URL parameter.
-   Retrieves the todo item with the specified id from the database.
-   Returns the todo item as JSON.

### Update a todo by id: `PUT /api/todos/:id`
-   Accepts the todo item's id as a URL parameter.
-   Accepts a JSON object in the request body containing fields to update (`title`, `description`, `status`, `due_date`, `UserId`).
-   Updates the specified todo item with the provided data and saves it to the database. 
- Returns the updated todo item as JSON.

### Delete a todo by id: `DELETE /api/todos/:id`
-   Accepts the todo item's id as a URL parameter.
-   Deletes the todo item with the specified id from the database.
-   Returns a JSON object with a message indicating the success of the deletion.

## User Routes
### Create a new user: `POST /api/users`
- Accepts a JSON object in the request body containing email, password, firstName, and lastName. 
- Hashes the password using bcrypt for security. 
- Creates a new user with the provided data and saves it to the database. 
- Returns the created user as JSON.

### Get all users: `GET /api/users`
- Retrieves all user items from the database.
- Returns an array of user items as JSON.
- Get all todos for a user: `GET /api/users/:id/todos`
- Accepts the user's id as a URL parameter.
- Retrieves all todo items associated with the specified user from the database.

### Update all todo statuses for a user: `PUT /api/users/:id/todos-status`
- Accepts the user's id as a URL parameter.
- Accepts a JSON object in the request body containing the status to update.
- Updates the status of all todo items associated with the specified user in the database.
- Returns a JSON object with a message indicating the success of the update.

### Delete all todos for a user: `DELETE /api/users/:id/todos`
- Accepts the user's id as a URL parameter.
- Deletes all todo items associated with the specified user from the database.
- Returns a JSON object with a message indicating the success of the deletion.

### Get a user by id: `GET /api/users/:id`
- Accepts the user's id as a URL parameter.
- Retrieves the user with the specified id from the database.
- Returns the user as JSON.

### Update a user: `PUT /api/users/:id`
- Accepts the user's id as a URL parameter.
- Accepts a JSON object in the request body containing fields to update (email, password, firstName, lastName).
- Updates the specified user with the provided data and saves it to the database.
- Returns the updated user as JSON.

### Delete a user: `DELETE /api/users/:id`
- Accepts the user's id as a URL parameter.
- Deletes the user with the specified id from the database.
- Returns a JSON object with a message indicating the success of the deletion.

**These routes provide basic CRUD functionality for managing todo items in your application. Make sure to add appropriate error handling and validation to these routes to ensure the reliability and security of your application.**

## Authentication Routes

The following routes are used for user authentication:

### Login a user: `POST /api/login`
- Accepts a JSON object in the request body containing email and password.
- Finds the user with the specified email in the database.
- Compares the provided password with the hashed password stored in the database.
- If the passwords match, generates a JWT token with the user's id and email.
- Returns the JWT token as JSON.
- If the email or password is incorrect, returns a 401 status code with an error message.
- If there is an error logging in, returns a 500 status code with an error message.

### Logout a user: `POST /api/logout`
- Requires authentication using the authenticateToken middleware. 
- Destroys the authentication token in the database to log the user out.

## Image Upload Routes

The following routes are used for uploading images:

### Upload an image: `POST /api/upload`
- Accepts a base64 encoded image in the request body. 
- Decodes the base64 data and saves the image to the uploads folder with a unique filename. 
- Returns the URL of the uploaded image.

### Serve uploaded images: `GET /uploads/:file`
- Serves the uploaded images stored in the uploads folder.
- Accepts the filename as a URL parameter and sends the corresponding image file.

<hr />

# Database Setup

A database named **todo_db** is created using **PostgreSQL**.

- After successfully installing PostgreSQL, you need to create a database and a user to connect to it.

```bash
sudo -u postgres psql
```
```bash
CREATE DATABASE todo_app;
CREATE USER todo_user WITH ENCRYPTED PASSWORD 'password123';
GRANT ALL PRIVILEGES ON DATABASE todo_app TO todo_user;
```
- The commands create a database named **todo_app** and define a user named **todo_user** with full access to the **todo_app** database._

**Note:** These config information (password, names for db & user etc.) are used as an example. You can use your own config information by creating **.env** file. I also add a **.env.example** file to the project.


### Database Connection & Server Setup
Add the above information to the config file for the database connection.

You can start the server by running `server.js` file:

```bash
node server.js
```

<hr />

# Usage

After setting up the frontend, backend, and database, you can start using the application. The application allows users to create, view, update, and delete todo items. Users can also upload images and files to their todo items.

Here are some example use cases for the application:

1. **Create a user account:** Users can create an account by providing their email, password, first name, and last name. The password is hashed for security.
2. **Log in:** Users can log in using their email and password. The application generates a JWT token for authentication.
3. **Create a todo item:** Users can create a new todo item by providing a title, description, due date, and tags. They can also upload an image for the todo item.
4. **View all todos for a user:** Users can view all their todo items in a list, including the title, description, due date, and status of each item.
5. **Update a todo item:** Users can update the title, description, due date, and status of a todo item. They can also add or remove tags and upload a new image.
6. **Delete a todo item:** Users can delete a todo item from the list.
7. **Log out:** Users can log out of the application, which destroys the JWT token.
8. **Upload an image:** Users can upload an image for a todo item. The image is stored in the uploads folder and served to the user.
9. **Serve uploaded images:** Users can view and download the images they uploaded for their todo items.
10. **Update all todo statuses for a user:** Users can update the status of all their todo items at once.
11. **Delete all todos for a user:** Users can delete all their todo items at once.

<hr />

# Screenshots

<img width="964" alt="Screenshot 2024-05-12 at 21 04 36" src="https://github.com/senaoz/playable-to-do-app/assets/66164676/9c9394f0-7c8b-49ff-928c-c78cae78f882">
<img width="964" alt="Screenshot 2024-05-12 at 21 04 39" src="https://github.com/senaoz/playable-to-do-app/assets/66164676/5334e277-a9f4-45ba-a671-a79b2ee51114">

<hr />

# Conclusion

This project demonstrates how to build a full-stack application using React.js, Node.js, Express.js, and PostgreSQL. The application provides basic CRUD functionality for managing todo items and user accounts. It also supports user authentication using JWT tokens and image uploads.

We can extend this project by adding more features, such as user roles, permissions, and notifications; also improve the user interface and add more styling to make the application more user-friendly.

If you have any questions or feedback, I would love to hear from you. Feel free to reach out to me on GitHub or LinkedIn. Thank you for reading, happy coding! 🚀



