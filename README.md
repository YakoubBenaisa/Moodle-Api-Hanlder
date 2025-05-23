# Moodle API

A Django-based API for accessing and interacting with Moodle e-learning platform data.

## Overview

This project provides a RESTful API interface to interact with Moodle learning management system data. It allows developers to authenticate, retrieve course information, manage content, and more through standardized API endpoints.

## Features

- User authentication with Moodle credentials
- Course content retrieval
- Chapter/section management
- Course structure navigation
- Resource/PDF document retrieval

Future planned features:
- User profile management
- Assignment submission and grading
- Forum integration
- Real-time notifications
- Analytics and reporting

## Getting Started

### Prerequisites

- Python 3.8+
- Django 5.1+
- Moodle instance access

### Installation

1. Clone the repository
```bash
git clone <repository-url>
cd moodle
```

2. Create and activate a virtual environment
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies
```bash
pip install -r requirements.txt
```

4. Run migrations
```bash
python manage.py migrate
```

5. Start the development server
```bash
python manage.py runserver
```

The API will be available at http://localhost:8000/api/

## API Documentation

The API provides the following endpoints:

- **Authentication**
  - POST `/api/login/` - Authenticate and receive a session token

- **Categories**
  - GET `/api/categories/` - List all available course categories

- **Courses**
  - GET `/api/courses/` - List all available courses
  - GET `/api/courses/{id}/` - Get details for a specific course

- **Chapters**
  - GET `/api/chapters/` - Get all chapters/sections for a course

- **Resources**
  - GET `/api/resources/` - Retrieve PDF and other resource files

For a complete API reference, import the `moodle_api_collection.json` file into Postman.

## Session Token Security

This API uses a secure session token approach to maintain authentication state:

- When a user logs in with valid Moodle credentials, the API generates a unique session token (UUID)
- The session token serves as a reference key to the user's Moodle session cookies stored in the server's cache
- No sensitive credentials are stored in the database or persistent storage
- Session tokens expire after 2 hours of inactivity
- All subsequent API requests require this session token as a query parameter
- The server reconstructs the authenticated session for each request using the cached cookies

This approach provides several security benefits:
- Credentials are never stored, only the cookies needed to maintain the Moodle session
- Session tokens are randomly generated UUIDs, making them difficult to guess
- The temporary cache storage ensures sessions are automatically cleaned up
- No sensitive data is exposed to the client beyond the session token itself

## Configuration

Edit `moodle/settings.py` to configure database settings, allowed hosts, and other Django settings.

## Security Notes

- The default settings include `DEBUG=True` which should be disabled in production
- Update the `SECRET_KEY` before deploying to production
- Configure proper `ALLOWED_HOSTS` for production environments
- Consider implementing rate limiting for the login endpoint
- For production, ensure HTTPS is enforced for all API endpoints

## License

MIT License

Copyright (c) 2023

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
