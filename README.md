# Requirements

- docker (at least 17.12.0+)
- docker-compose (at least 1.18.0)
- docker-hostmanager
- git

## Docker name resolution

In order to access the application on your browser, your host machine must be able to resolve the host name of your container.
We're using docker-hostmanager to manage the hosts file entries for all docker-compose environments.

```
$ docker run -d --name docker-hostmanager --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v /etc/hosts:/hosts iamluc/docker-hostmanager
```

Setup
=====

* Copy the repository content (please don't fork it so that there is no link to forked repositories someone might look up the solution at)
* Start the containers ```docker-compose up``` 
* Initialize the database ```docker-compose run django migrate```
* Create a Google OAuth client ID (https://developers.google.com/identity/sign-in/web/devconsole-project) and add http://testcase.rh-dev.eu:8001 to "Authorized JavaScript origins"
* Save the client ID in the Django settings file (backend/settings.py) to the variable GOOGLE_CLIENT_ID and use the same one in the frontend app
* Implement the frontend against the API
* Extend the readme on how to build and run the frontend, the JS frontend webserver should run on port 8001 (http://testcase.rh-dev.eu:8001)

Authorization
=============

The OAuth token generated on the client side must be sent with each request to the server in the Authorization header.

```Authorization: Token thisIsMyOAuthToken```

API endpoints
=============

The API provides GET, PUT, POST, PATCH, DELETE and OPTIONS to manage all user related needs

http://testcase.rh-dev.eu:8000/api/users to list and http://testcase.rh-dev.eu:8000/api/users/{id} to manage single users
