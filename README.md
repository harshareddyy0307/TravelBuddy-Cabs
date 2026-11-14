# TravelBuddy Cabs — Complete Project

A complete campus shuttle management application built with Node.js, Express, SQLite and a responsive dashboard UI.

## Requirements
- Node.js 22.5 or later. Node.js 24 is suitable.
- VS Code (recommended)

This project uses Node.js built-in `node:sqlite`. It does not use `better-sqlite3`, so Visual Studio C++ Build Tools and Python compilation setup are not required.

## Run the project
1. Extract the ZIP.
2. Open the **TravelBuddy_Cabs_Full_Project** folder itself in VS Code. `package.json` must be visible at the top level.
3. Open Terminal in VS Code.
4. Run:
   ```bash
   npm install
   npm start
   ```
5. Open http://localhost:3000

Stop the server with Ctrl+C.

## Included modules
- Overview dashboard with live database counts and recent reservations
- Passenger management: create, search, update
- Shuttle route management: create, search, filter by time slot, update
- Reservations: create, search, filter, cancel
- SQLite persistence
- REST API with JSON responses and appropriate HTTP status codes
- Form validation and readable error messages
- Responsive desktop and mobile UI

## Reservation rules
- A passenger can have a maximum of 3 active reservations.
- A fourth active reservation returns HTTP 409 with `Limit of 3 reached`.
- Cancelling a reservation changes its status to `cancelled`, freeing one active booking slot.
- A shuttle cannot be booked after its capacity is reached.

## Main API endpoints
| Method | Endpoint | Purpose |
|---|---|---|
| GET | `/api/dashboard` | Dashboard statistics and recent reservations |
| GET | `/api/passengers` | List/search passengers |\n| GET | `/api/passengers/:id` | Get one passenger |\n| POST | `/api/passengers` | Create passenger |
| PUT, DELETE | `/api/passengers/:id` | Update/delete passenger (deletion blocked if reservation history exists) |
| GET | `/api/shuttles` | List/search/filter shuttles |\n| GET | `/api/shuttles/:id` | Get one shuttle |\n| POST | `/api/shuttles` | Create shuttle |
| PUT, DELETE | `/api/shuttles/:id` | Update/delete shuttle (deletion blocked if reservation history exists) |
| GET, POST | `/api/reservations` | List/search/filter and create reservations |
| PATCH | `/api/reservations/:id/cancel` | Cancel an active reservation |
| GET | `/api/health` | API health check |

### Example passenger JSON
```json
{"name":"Asha Kumar","email":"asha@example.com","phone":"+91 98765 43210"}
```

### Example shuttle JSON
```json
{"name":"Campus Express","slot":"Morning","route":"Main Gate - Academic Block","departureTime":"08:30 AM","capacity":30}
```

### Example reservation JSON
```json
{"passengerId":1,"shuttleId":1}
```

## Project structure
```text
TravelBuddy_Cabs_Full_Project/
  package.json
  server.js
  src/
    database.js
    validation.js
    routes/
      passengerRoutes.js
      shuttleRoutes.js
      reservationRoutes.js
  public/
    index.html
    styles.css
    app.js
  README.md
```

The SQLite database `travelbuddy.db` is generated automatically the first time the server starts.
