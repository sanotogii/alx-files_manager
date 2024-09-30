# ALX Files Manager

## Overview
The Files Manager is a web-based file management system with features for user authentication, file uploads, image processing, and more.

## Technologies
- Node.js, Express
- Redis, MongoDB
- Bull (for background processing)
- Image-thumbnail, SHA1, uuidv4

## Setup
1. Clone the repo: `git clone https://github.com/alx-files_manager.git`
2. Install dependencies: `npm install`
3. Start Redis and MongoDB
4. Start the app: `npm start`
5. Start the worker: `npm run start-worker`

## Key Endpoints
| Endpoint                  | Method | Description                                  |
|---------------------------|--------|----------------------------------------------|
| `/connect`                | `GET`  | Authenticate user with Basic Auth            |
| `/disconnect`             | `GET`  | Logout user                                  |
| `/users/me`               | `GET`  | Retrieve authenticated user info             |
| `/files`                  | `POST` | Upload a new file or create a folder         |
| `/files/:id`              | `GET`  | Retrieve file/folder details                 |
| `/files`                  | `GET`  | List files/folders with pagination           |
| `/files/:id/data`         | `GET`  | Retrieve file content, supports thumbnail sizes |

**Authentication:** Use `Authorization: Basic <Base64-encoded email:password>` for `/connect` and `X-Token: <token>` for other endpoints.

## Thumbnail Generation
- When an image is uploaded, a job is added to a `fileQueue` using Bull.
- Worker generates thumbnails (100px, 250px, 500px) and saves them locally.
- `/files/:id/data?size=<size>` fetches thumbnails (size options: 100, 250, 500).

## Welcome Email
- `userQueue` processes a welcome email job when a new user registers.
- Worker logs "Welcome <email>!" to the console.

## Running Tests
The project includes tests for key functionalities:
- **Core tests:** Redis and MongoDB clients
- **API endpoints:** Status, authentication, user management, file management, and more

Run tests using: `npm test`
