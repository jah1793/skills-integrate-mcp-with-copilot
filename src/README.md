# Mergington High School Activities API

A super simple FastAPI application that allows students to view extracurricular activities and teachers to manage signups.

## Features

- View all available extracurricular activities
- Teacher-only signup and unregistration

## Getting Started

1. Install the dependencies:

   ```
   pip install fastapi uvicorn
   ```

2. Configure the teacher account in the server environment. Do not commit credentials:

   ```
   export TEACHER_USERNAME=teacher
   export TEACHER_PASSWORD='use-a-unique-secret-password'
   ```

   Configure these values through your deployment's secret manager in production.
   Serve the application over HTTPS so credentials are protected in transit.

3. Run the application:

   ```
   uvicorn app:app --app-dir src --reload
   ```

4. Open your browser and go to:
   - API documentation: http://localhost:8000/docs
   - Alternative documentation: http://localhost:8000/redoc

## API Endpoints

| Method | Endpoint                                                          | Description                                                         |
| ------ | ----------------------------------------------------------------- | ------------------------------------------------------------------- |
| GET    | `/activities`                                                     | Get all activities and current participants (public)                |
| POST   | `/auth/verify`                                                    | Verify teacher credentials using HTTP Basic authentication          |
| POST   | `/activities/{activity_name}/signup?email=student@mergington.edu` | Sign up a student (teacher authentication required)                  |
| DELETE | `/activities/{activity_name}/unregister?email=student@mergington.edu` | Unregister a student (teacher authentication required)          |

## Data Model

The application uses a simple data model with meaningful identifiers:

1. **Activities** - Uses activity name as identifier:

   - Description
   - Schedule
   - Maximum number of participants allowed
   - List of student emails who are signed up

2. **Students** - Uses email as identifier:
   - Name
   - Grade level

All data is stored in memory, which means data will be reset when the server restarts.
