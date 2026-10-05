# EpicBook Environment Variables and Ports

**Name:** Peace Nwadinachi Offor
**Assignment:** DMI Cohort 3 - Assignment 7

## Reverse Proxy
- Service: Nginx
- Public port: 80
- Internal port: 80
- Network: front-tier

## Frontend
- Runtime: Nginx
- Internal port: 80
- Published host port: None
- Network: front-tier

## Backend
- Runtime: Node.js / Express
- Internal port: <DISCOVERED PORT>
- Published host port: None
- Networks: front-tier, back-tier

## Database
- Engine: MySQL
- Internal port: 3306
- Published host port: None
- Network: back-tier
- Persistent data path: /var/lib/mysql
- Named volume: db_data

## Environment Variable Names
- <DISCOVERED VARIABLE NAME>
- <DISCOVERED VARIABLE NAME>
- <DISCOVERED VARIABLE NAME>
- <DISCOVERED VARIABLE NAME>

No real credentials are stored in this document.

## Health Checks
- Database: mysqladmin ping
- Backend: HTTP /health
- Frontend: HTTP request to Nginx
- Reverse proxy: HTTP request through /health

## Network Design
- front-tier connects the reverse proxy, frontend, and backend.
- back-tier connects the backend and database.
- back-tier is an internal Docker network.
- Only the reverse proxy publishes a host port.
