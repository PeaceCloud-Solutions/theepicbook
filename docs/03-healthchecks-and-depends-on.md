# EpicBook Health Checks and Startup Dependencies

**Deployed by:** Peace Nwadinachi Offor

## Health Checks

### Database

The MySQL database uses `mysqladmin ping` to verify that the
database server is ready to accept connections.

### Backend

The backend exposes `/health` on internal port 8080.
Docker uses curl to verify that this endpoint returns a successful
HTTP response.

### Frontend

The frontend runs Nginx and serves the EpicBook static assets.
Its health check requests `/assets/css/style.css` to verify that
Nginx is running and frontend content is available.

### Reverse Proxy

The reverse proxy uses Nginx and verifies the application health
endpoint through `http://127.0.0.1/health`. The IPv4 loopback
address is used because Nginx listens on IPv4 inside the container.

## Startup Dependency Order

1. The MySQL database starts and must become healthy.
2. The backend waits for the database using
   `condition: service_healthy`.
3. The frontend starts and must successfully serve its static content.
4. The reverse proxy waits for both the frontend and backend using
   `condition: service_healthy`.
5. The reverse proxy becomes the only public entry point on port 80.

This startup sequence prevents dependent services from being treated
as ready before the services they require are healthy.
