# Devops API App


### install the node packages in the web container:
```sh
→ docker-compose run api npm install
```
> Docker will download all of the images for the container.

### start up the app:
```sh
→ docker-compose up
```

###  NOTE this app use two env variables:

- PORT: the listening PORT
- DB: the postgresql url to connect

This two variables need to be populate with docker-compose (API_PORT, API_DB).
