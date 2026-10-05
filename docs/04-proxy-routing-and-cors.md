# EpicBook Reverse-Proxy Routing and CORS

**Deployed by:** Peace Nwadinachi Offor

## Reverse Proxy

Nginx is used as the reverse proxy and is the only public entry
point for the EpicBook Docker Compose stack.

Only Nginx publishes host port 80. The frontend, backend, and
MySQL database remain accessible only through the Docker networks.

## Routing

### Application Pages

Requests for EpicBook application pages are routed by Nginx to
the backend service using its Docker Compose service name and
internal port 8080.

Examples of application routes include `/`, `/cart`, and
`/gallery`.

### Static Assets

Requests under `/assets/` are routed to the frontend Nginx
container, which serves the application's static files.

The `/assets/css/style.css` resource was successfully tested
through the reverse proxy.

### API Requests

EpicBook API requests are routed through the public Nginx reverse
proxy to the backend service on internal port 8080.

The application provides the `/api/cart` API endpoint. This
endpoint was tested through the reverse proxy without exposing
backend port 8080 directly to the host.

### Health Endpoint

Requests to `/health` are forwarded by Nginx to the backend
health endpoint:

`http://backend:8080/health`

This provides a public application health check while keeping the
backend container private.

## Same-Origin Routing

Users access EpicBook through one public origin:

`http://16.170.240.216`

Application pages, API requests, static assets, and health checks
are all accessed through the same Nginx reverse proxy.

## CORS

Separate cross-origin browser access is not required for this
deployment because the application and API are presented to the
browser through the same public origin.

Nginx performs the internal routing between the frontend and
backend services. The browser does not need to connect directly
to the backend container on port 8080.

This same-origin design reduces CORS complexity and keeps the
internal Docker services from being exposed publicly.
