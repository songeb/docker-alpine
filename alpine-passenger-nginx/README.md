### Base Image: Alpine Passenger + Nginx Module
- **Build Image:**
```
docker build -t phusion-passenger-nginx-alpine:latest .
```
- **Run Container:**
```
docker run -d -p 80:80 --name phusion-passenger-nginx-alpine phusion-passenger-nginx-alpine:latest
```
----------
