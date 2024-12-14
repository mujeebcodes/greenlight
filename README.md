# Greenlight Application

Greenlight is a JSON API for managing movie information, developed using Go. Inspired by the Open Movie Database API, this project demonstrates modern API design, clean architecture, and best practices in web development with Go.

---

## Features

The Greenlight API supports the following actions:

### Movies
- **GET /v1/movies**: List all movies.
- **POST /v1/movies**: Add a new movie.
- **GET /v1/movies/:id**: Retrieve a specific movie's details.
- **PATCH /v1/movies/:id**: Update a movie's details.
- **DELETE /v1/movies/:id**: Delete a movie.

### User Management
- **POST /v1/users**: Register a new user.
- **PUT /v1/users/activated**: Activate a user.
- **PUT /v1/users/password**: Update a user's password.

### Tokens
- **POST /v1/tokens/authentication**: Generate an authentication token.
- **POST /v1/tokens/password-reset**: Request a password reset.

### Miscellaneous
- **GET /v1/healthcheck**: Retrieve application status and version.
- **GET /debug/vars**: Access application metrics.

---

## Setup

### Prerequisites
1. **Go**: Ensure Go 1.23 or later is installed.
    - [Install Go](https://golang.org/doc/install)
2. **PostgreSQL**: Set up a PostgreSQL database.
3. **Additional Tools**:
    - `curl` for testing HTTP requests.
    - `hey` for load testing: `go install github.com/rakyll/hey@latest`
    - `git` for version control.

### Directory Structure
The project structure adheres to the following layout:
```
.
├── bin/            # Compiled application binaries.
├── cmd/api/        # Application-specific code.
├── internal/       # Ancillary packages (database interactions, utilities, etc.).
├── migrations/     # SQL migration files.
├── remote/         # Server configuration files.
├── go.mod          # Module dependencies.
├── Makefile        # Automation recipes.
```

### Installation
1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd greenlight
   ```
2. Initialize the project:
   ```bash
   go mod tidy
   ```
3. Configure environment variables for database connectivity and other settings:
   ```bash
   export GREENLIGHT_DB_DSN="user:password@/dbname"
   export GREENLIGHT_ENV="development"
   ```
4. Start the server:
   ```bash
   go run ./cmd/api
   ```

---

## Usage

### API Example
To check the server health:
```bash
curl http://localhost:4000/v1/healthcheck
```
Expected Response:
```json
{
  "status": "available",
  "environment": "development",
  "version": "1.0.0"
}
```

### Running Migrations
Apply database migrations using:
```bash
make migrate
```

---

## Deployment
The application can be deployed to a Linux server on Digital Ocean or other platforms. Ensure to:
1. Configure a reverse proxy (e.g., [Caddy](https://caddyserver.com/)).
2. Set up the application as a background service using systemd.
3. Automate tasks like migration execution and binary builds via Makefile.

---

## Contributing
Pull requests and issues are welcome! Please adhere to the Go community's style guidelines.

---

## Acknowledgments
This project follows Alex Edwards' book [*Let's Go Further*](https://lets-go-further.alexedwards.net/), which serves as a practical guide for building robust Go applications.
