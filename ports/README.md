Build and run my-app container:
```
docker build -t my-app .
docker run --name my-app -d my-app
```

Get my-app IP address:
```
docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' my-app
```
(for example, `172.17.0.2`).

Build and run proxy container:
```
docker build -t my-proxy .
docker run --name my-proxy -d -p 8080:80 --env ReverseProxy__Clusters__my-cluster__Destinations__my-destination__Address=http://172.17.0.2/ my-proxy
```

Send a request:
```http
### GET localhost request
GET http://localhost:8080/
```