# Backend Scheduler API

## Overview

This backend service is designed to handle scheduled tasks and send emails based on specific dates. It includes endpoints for saving user data and retrieving all stored data. The service uses Node.js with Express, Nodemailer for sending emails, and Cron for scheduling tasks.

## Features

- **Add Data**: Save user data including email and a message.
- **Get Data**: Retrieve all stored user data.
- **Scheduled Email**: Send an email to users based on the date stored in their data.

## API Endpoints

### 1. Save Data

- **URL**: `https://back-scheduler.onrender.com/message/send`
- **Method**: `POST`
- **Description**: Saves user data into the database.
- **Request Body**:
  ```json
  {
    "email": "user@example.com",
    "date": "YYYY-MM-DD",
    "message": "Your message here"
  }
  ```
- **Response**:
  - Success:
    ```json
    {
      "success": true,
      "message": "Data saved in database"
    }
    ```
  - Failure:
    ```json
    {
      "success": false
    }
    ```

### 2. Get All Data

- **URL**: `https://back-scheduler.onrender.com/message/data`
- **Method**: `GET`
- **Description**: Retrieves all stored user data.
- **Response**:
  ```json
  {
    "data": [
      {
        "email": "user@example.com",
        "date": "YYYY-MM-DD",
        "message": "Your message here"
      },
      ...
    ]
  }
  ```

## Cron Job

A scheduled task runs every day at 10:30 AM (server time) to check if any users have a date matching the current date. If a match is found, an email is sent to the user with the provided message.

## Configuration

1. **Environment Variables**: Make sure to set up your environment variables in a `.env` file.
   ```plaintext
   GMAIL_USER=your-email@gmail.com
   PASSWORD=your-email-password
   ```

2. **Dependencies**:
   - `nodemailer`: For sending emails.
   - `dotenv`: For loading environment variables.
   - `cron`: For scheduling tasks.
   - `mongoose` or other database module (assumed as `userModule` in your code).
