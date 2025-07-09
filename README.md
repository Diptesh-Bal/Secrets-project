# Secrets Project: 

This project is a Node.js/Express web application that allows users to register, log in (locally or with Google), submit secrets, and view secrets. It demonstrates authentication, session management, and secure password storage.

---

## APIs and Functionality

### Main Endpoints

- `GET /` — Home page.
- `GET /register` — Registration page.
- `POST /register` — Register a new user (email, password). Hashes password and stores in the database.
- `GET /login` — Login page.
- `POST /login` — Log in an existing user (local strategy).
- `GET /logout` — Log out the current user.
- `GET /secrets` — View the user's secret (requires authentication).
- `GET /submit` — Page to submit a new secret (requires authentication).
- `POST /submit` — Submit a secret for the logged-in user.
- `GET /auth/google` — Start Google OAuth login.
- `GET /auth/google/secrets` — Google OAuth callback.

### Authentication

- Local authentication using email and password (with bcrypt hashing).
- Google OAuth 2.0 authentication.
- Session management with Passport.js.

---

## Database

- **Type:** PostgreSQL
- **Integration:**
  - Uses the `pg` Node.js package to connect and query the database.
  - User data (email, hashed password, secret) is stored in a `users` table.
  - Example schema:
    ```sql
    CREATE TABLE users (
      id SERIAL PRIMARY KEY,
      email VARCHAR(255) UNIQUE NOT NULL,
      password VARCHAR(255) NOT NULL,
      secret TEXT
    );
    ```
- **Configuration:**
  - Database connection details are set in your environment variables or configuration file.
 
---

## Folder Structure

```
Secrets-project/
│
├── css/
│   └── styles.css
├── views/
│   ├── home.ejs
│   ├── register.ejs
│   ├── partials/
│   │   ├── header.ejs
│   │   └── footer.ejs
├── index.js
├── solution.js
├── package.json
├── solution-queries.sql
├── README.md
```

- `css/`: Contains styling files.
- `views/`: EJS templates for web pages and partials.
- `index.js`, `solution.js`: Main server files.
- `package.json`: Project dependencies.
- `solution-queries.sql`: SQL migration/query file.
- `README.md`: Project documentation.

---

## How to Run the Server

1. **Install dependencies:**
   ```bash
   npm install
   ```
2. **Set up your PostgreSQL database:**
   - Create a database and the `users` table as shown above.
   - Set your database credentials in environment variables or a config file.
3. **Set up Google OAuth credentials:**
   - Register your app with Google and set `GOOGLE_CLIENT_ID` and `GOOGLE_CLIENT_SECRET` in your environment.
4. **Start the server:**
   ```bash
   node solution.js
   # or, for development with auto-reload:
   npx nodemon solution.js
   ```
5. **Visit:**
   - [http://localhost:3000](http://localhost:3000)

---

## How to Interact with the API

- **Web Interface:**
  - Use the provided EJS views for registration, login, submitting secrets, and viewing secrets.
- **API Endpoints:**
  - You can use tools like Postman or curl to interact with the POST endpoints (`/register`, `/login`, `/submit`).
  - Example registration:
    ```bash
    curl -X POST http://localhost:3000/register -d "username=test@example.com&password=yourpassword"
    ```
  - Example login:
    ```bash
    curl -X POST http://localhost:3000/login -d "username=test@example.com&password=yourpassword"
    ```
  - Example submit secret (after login, with session cookie):
    ```bash
    curl -X POST http://localhost:3000/submit -d "secret=My secret" --cookie "connect.sid=YOUR_SESSION_COOKIE"
    ```
---

## Notes

- Make sure to configure your environment variables for database and Google OAuth.
