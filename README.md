# Memories API

REST API for **Memories**, a small app where users share photo posts with a title, message and tags, and can like them.

This is the server side of a MERN learning project I built in 2021 to practice the full stack end to end. The React + Redux client is in [memories-client](https://github.com/hasanugr/memories-client).

## Tech Stack

- **Node.js** + **Express** for the REST API
- **MongoDB Atlas** with **Mongoose** for data modeling
- **dotenv** for configuration, **cors** for cross-origin requests, **nodemon** for development

## API Endpoints

Base URL: `http://localhost:5000`

| Method | Endpoint | Description |
|---|---|---|
| GET | `/posts` | List all posts |
| POST | `/posts` | Create a post |
| PATCH | `/posts/:id` | Update a post |
| DELETE | `/posts/:id` | Delete a post |
| PATCH | `/posts/:id/likePost` | Increase the like count of a post |

Invalid IDs return `404`, and validation errors on create return `409`.

### Post model

| Field | Type | Notes |
|---|---|---|
| `title` | String | |
| `message` | String | |
| `creator` | String | |
| `tags` | [String] | |
| `selectedFile` | String | Image stored as a base64 string |
| `likeCount` | Number | Default `0` |
| `createdAt` | Date | Set on creation |

## Getting Started

**Requirements:** Node.js and a MongoDB connection string (a free MongoDB Atlas cluster works).

```bash
git clone https://github.com/hasanugr/memories-server.git
cd memories-server
npm install
cp .env.example .env
```

Edit `.env`:

```env
PORT=5000
CONNECTION_URL=your_mongodb_connection_string
```

Start the server:

```bash
npm start
```

Quick test:

```bash
curl -X POST http://localhost:5000/posts \
  -H "Content-Type: application/json" \
  -d '{"title":"First post","message":"Hello","creator":"Hasan","tags":["test"]}'
```

## Project Structure

```
├── index.js              # App setup, middleware, DB connection
├── routes/posts.js       # Route definitions
├── controllers/posts.js  # Request handlers
└── models/postMessage.js # Mongoose schema
```

## Known Limitations

This was a learning project, so some parts are kept simple on purpose:

- No authentication: anyone can edit or delete any post.
- Images are stored as base64 strings in the database. A production app would use object storage (e.g. S3 or Supabase Storage) and save only the URL.
- Input validation and error handling are minimal.
