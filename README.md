# Video Game Diary

A Letterboxd-inspired web application for discovering video games and keeping track of what you have played, are currently playing, or want to play. Built with Angular, it uses the RAWG API for game information and an Express/MongoDB backend to store diary entries.

## Features

- Browse games and navigate through paginated results.
- Search for games by title.
- View game descriptions, artwork, release dates, and RAWG ratings.
- Save games as **Played**, **Playing**, or **Want to Play**.
- Give games a personal rating from **1 to 5 stars** when adding them.
- View saved games in a library grouped by status.
- Remove games from the library.
- Receive success or error messages when adding or removing games.
- Dark interface styled with Bootstrap and custom CSS.

## Technology

| Layer        | Technologies                                                  |
| ------------ | ------------------------------------------------------------- |
| Frontend     | Angular 21, TypeScript, Angular Router, Angular Signals, RxJS |
| Styling      | Bootstrap 5, custom CSS                                       |
| Game data    | [RAWG API](https://rawg.io/apidocs)                           |
| Backend      | Node.js, Express 5, CORS, dotenv                              |
| Database     | MongoDB, Mongoose 9                                           |
| Unit testing | Vitest through Angular CLI                                    |

## Getting started

### Prerequisites

- Node.js compatible with Angular 21: `^20.19.0`, `^22.12.0`, or `>=24.0.0`.
- npm.
- A RAWG API key.
- A MongoDB connection string, using a local database or MongoDB Atlas.

### 1. Clone the repository

```bash
git clone https://github.com/S00271020/videogame-diary-angular.git
cd videogame-diary-angular
npm ci
```

### 2. Configure the frontend

Update `src/environments/environment.ts` with your RAWG API key and the local backend URL:

```typescript
export const environment = {
  production: false,
  rawgApiKey: 'YOUR_RAWG_API_KEY',
  backendApiUrl: 'http://localhost:5050',
};
```

The checked-in configuration contains a placeholder RAWG key and an AWS API Gateway backend URL. Replace these values to use your own local setup. The supplied `environment.example.ts` shows the API key field, but you also need `backendApiUrl` as shown above.

### 3. Configure the backend

Install the backend dependencies:

```bash
cd backend
npm ci
```

Copy `backend/.env.example` to `backend/.env` and supply your database connection string:

```dotenv
MONGO_URI=mongodb://127.0.0.1:27017/videogame-diary
PORT=5050
```

For MongoDB Atlas, replace `MONGO_URI` with your Atlas connection string.

In `backend/server.js`, change the `origin` value inside `corsOptions` to allow the local Angular development server:

```javascript
origin: 'http://localhost:4200',
```

The current value allows the deployed Amplify frontend. Without this change, browser requests from the local frontend to your backend will be blocked by CORS.

### 4. Start the application

In a terminal inside `backend/`:

```bash
npm start
```

The backend starts listening on port `5050` after connecting to MongoDB. Visit `http://localhost:5050/` to check for the response `API is running`.

In a second terminal, from the repository root:
