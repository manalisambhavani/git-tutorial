# 📘 Express + Sequelize + JWT Authentication Notes

This document explains how database operations and JWT-based authentication & authorization work in your Node.js + TypeScript application using Express and Sequelize.

---

## 1. 🗃️ Database Operations (Using Sequelize)

Sequelize is an ORM (Object Relational Mapper) that helps you interact with SQL databases (like PostgreSQL) using JavaScript/TypeScript syntax instead of raw SQL.

### ✅ Steps Involved:

1. **Connecting to the DB**

   ```ts
   export const sequelize = new Sequelize(
     'express-tutorial',   // Database name
     'postgres',           // Username
     'postgres',           // Password
     {
       host: 'localhost',
       port: 5433,
       dialect: 'postgres',
       logging: false
     }
   );
   ```

   This creates a connection with the PostgreSQL database.

2. **Defining a User Model**

   ```ts
   const User = sequelize.define('user', {
     id: {
       type: DataTypes.INTEGER,
       autoIncrement: true,
       primaryKey: true,
     },
     username: {
       type: DataTypes.STRING,
       allowNull: false,
       unique: true,
     },
     password: {
       type: DataTypes.STRING,
       allowNull: false,
     },
   });
   ```

   The model maps to a `users` table in PostgreSQL. The `username` field is unique, preventing duplicates.

3. **Synchronizing the Model with the DB**

   ```ts
   await sequelize.sync({ alter: true });
   ```

   This creates or alters the table schema in the database to match the model.

4. **Signup Flow**

   * First, checks if a user with the same username exists.
   * If not, creates a new user using:

     ```ts
     const newUser = await User.create({ username, password });
     ```

5. **Login Flow**

   * Checks if credentials match using:

     ```ts
     const user = await User.findOne({ where: { username, password } });
     ```

---

### 🧭 Sequelize Flow Diagram

```text
┌────────────┐
│  Express   │
└────┬───────┘
     │
     ▼
┌───────────────┐
│  Sequelize    │
└────┬──────────┘
     │
     ▼
┌───────────────┐
│  PostgreSQL   │
└───────────────┘
```

---

## 2. 🔐 JWT Authentication & Authorization

JWT (JSON Web Token) is a compact and secure way to transmit data, especially for authentication and authorization.

---

### ✳️ Basic Concepts

| Term            | Meaning                                                                 |
| --------------- | ----------------------------------------------------------------------- |
| Authentication  | Verifying **who** the user is (e.g., via login credentials).            |
| Authorization   | Verifying **what** the user is allowed to do (using valid token).       |
| `signToken()`   | A utility function that generates a JWT token.                          |
| `verifyToken()` | A utility function that verifies if the provided token is valid or not. |

---

### ✅ Signup & Login Flow with Token Generation

#### Signup

```ts
const token = signToken({ userId: newUser.id });
```

* After user creation, a JWT is generated and sent to the client.
* The client stores this token for future use.

#### Login

```ts
const token = signToken({ userId: user.id });
```

* If credentials match, generate and send JWT.

---

### ✅ Profile Access with Token Verification

```ts
const decoded = verifyToken(token);
```

* On routes like `/profile`, the token is extracted from query string.
* If token is valid, allow access. Otherwise, return 401 Unauthorized.

---

### 🔁 Token Flow Diagram

```text
   ┌────────────┐
   │   Client   │
   └────┬───────┘
        │ Signup/Login
        ▼
   ┌────────────┐
   │   Server   │
   └────┬───────┘
        │ signToken()
        ▼
   ┌────────────┐
   │    JWT     │─────> stored on client
   └────────────┘

▶ Later on protected route (e.g., /profile?token=...):
  - verifyToken(token)
  - If valid → return data
  - If invalid → return 401 Unauthorized
```

---

## 3. 🔧 Utility Functions (`signToken`, `verifyToken`)

These are typically created in a separate file like `jwt.ts`.

```ts
import jwt from 'jsonwebtoken';

const SECRET_KEY = 'your-secret-key';

export function signToken(payload: object): string {
  return jwt.sign(payload, SECRET_KEY, { expiresIn: '1h' });
}

export function verifyToken(token: string): object | null {
  try {
    return jwt.verify(token, SECRET_KEY);
  } catch {
    return null;
  }
}
```

