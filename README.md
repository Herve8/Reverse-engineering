# Reverse-engineering

## Password authentication and logging into a form

# Business Context

When joining a new team, you will be expected to inspect a lot of code that you have never seen before. Rather than having a team member explain every line for you, you will dissect the code by yourself, saving any questions for a member of your team.

## About this app

This app allows users to create an account, log into the account and sign back out securely. All user data being enterred is stored in the "passport_demo" mysql database.

# Acceptance Criteria

GIVEN a Node.js application using Sequelize and Passport
WHEN I follow the walkthrough
THEN I understand the codebase

# Functionality of the app

The user starts by either logging in as a new user where the user creates a username and password.
After successfully creating the username and password, the user logs into the website.
After successfully logging into the website the user is granted by a welcoming page, "Welcome test@gmail.com", which uses the
user's email address in the greeting message.

# Technology used

mysql2, passport, sequelize, bcryptjs, express, express-session,

# Steps to run the app

1)To start using this app, please pull from gitlab into your local storage.
2)Create a mysql db called "passport_demo".
3)Open the app in Visual Studio.
4)Open config.json and change the developement database by inserting your information for your mysql database, that is username and password
5)Go to your app in Visual Studio, right-click on any file and choose "Open in Integrated Terminal".
6)Type and run "npm i" to install all the npm node packages and dependencies
7)In terminal, type and run "node server.js" and the server will connect successfully
8)To open the browser, select the command key and at the same time click on "localhost:8080" at the bottom
of Visual Studio where your app is executing
9)The logging page will appear and you can start using the app

# --DISSECTING THE CODE--

# Configs

config.json
Loads the default configuration file.
Loads environment specific configuration file declared by user and overrides defaults;
It also uses environment variables, and command-line arguments to override data from configuration files.

package-lock.json
Keeps track of the exact version of every package that is installed so that an app is able to work even if packages are updated.

---

# Middleware

var app = express();
app.use(express.urlencoded({ extended: true }));
app.use(express.json());
app.use(express.static("public"));

The codes above shows a middleware with a mount path to the public folder.
The function is executed every time the app receives a request.
express() creates a new instance of express that you can then assign to a variable and interact with the public folder.

app.use(express.urlencoded()
Is an inbuilt method in express to deal with incoming Request Object as strings or arrays.

isAuthenticated.js
Again is a middleware that acts as a gatekeeper to restrict users who are not allowed o visit a page if not logged in. If the user is not logged in it will re-direct user to the logging page.

passport.js
Configures how the logging should be. the logging form requires a username/email and password to enable a user to successfully log in.

---

# Models

index.js
connects to database and imports users data using sequelize, meaning that it uses code first to create and populate the database

user.js
Main function is to encrypt users password using crypt, which is a password hasing function.

---

# Routes

api-routes.js
Acts as a gatekeeper while users are signing in. It checks the authentication of users signing in or logging in through the use of the Sequelize User Model.
If the user is created successfully, proceed to log the user in, otherwise send back an error.
If the user has valid login credentials, send them to the members page, otherwise the user will be sent an error

html-routes.js
Uses routes that check whether the users have a valid account before directing them to the Members page.

server.js
requires npm packages, sets up PORT, creates express and configures middleware, creates routes and syncs database. Also provides the status of the server while successfully connected or throws an error in the event of unsuccessful connections.
