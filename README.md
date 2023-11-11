# Rust API, Postgres and Docker

Created a REST API with Rust, Serde, Postgres and Docker.

## Installation

### Run the Postgres container

First, run the postgres container:

```bash
docker-compose up -d db
```

This will pull (download) the image from DockerHub and run it on our machine.

#### To see the logs, you can type

```bash
docker-compose logs db
```

If you have something like this, it means that the database is up and running in the container (the last line of the logs should say: "database system is ready to accept connections")

### Build the Rust app Image

t's time to build the Rust app image. We will use the docker-compose build command.
This will build the image using the Dockerfile we created before.

(Note: we might type docker compose up, but by doing that, we would skip understanding what's happening. In a nutshell, when we type docker compose up, Docker builds the images if needed and then runs the containers).

```bash
docker compose build
```

This takes time because we are building the Rust app inside the image.

After ~150 seconds (!), we should have the image built.

### Build the Rust app Image

Now we can run the Rust container:

```bash
docker compose up rustapp
```

You can check both containers by opening another terminal and typing:

```bash
docker ps -a
```

Lastly, you can check the postgres database by typing:

```bash
docker exec -it db psql -U postgres
\dt
select * from users;
```

The app has been running. It's now time to test our application.

## 🧪 Test the application

#### 📝 Test the db connection

Since we don't have a dedicated endpoint to test the db connection, we will make a

```bash
GET request to http://localhost:8080/users
```

The output should be []. This is correct, as the database is empty.

#### 📝 Create a new user

To create a new user, make a POST request to

```bash
GET request to http://localhost:8080/users
```

with the following body:

⚠️ Add the header

```bash
Content-Type: application/json
```

in the request

```bash
{
    "name": "aaa",
    "email": "aaa@mail"
}
```

Create two more users with the following bodies at the same endpoint making a

```bash
POST request to http://localhost:8080/users
```

with the following body:

```bash
{
    "name": "jhon",
    "email": "jhon@mail.com"
}
{
    "name": "jane",
    "email": "jane@mail.com"
}
```

#### 📝 Get all users

To get all the users, make a

```bash
GET request to http://localhost:8080/users
```

#### 📝 Get a single user (with error handling)

To get a single user, we can specify the id in the URL.

For example, to get the user with id 1, we can make a

```bash
GET request to http://localhost:8080/users/1
```

Notice that if we try to get a user with an id that doesn't exist, we get an error "User not found".

Make a

```bash
GET request to http://localhost:8080/users/10
```

And if we try to get a user py using a string instead of an integer, we also get an error "Internal Error"

Make a

```bash
GET request to http://localhost:8080/users/ss
```

#### 📝 Update a user

We must pass an id in the URL and a body with the new data to update an existing user.

For example, make a

```bash
PUT request to http://localhost:8080/users/2
```

with the following body:

```bash
{
    "name": "jane update",
    "email": "janeupdate@mail.com"
}
```

#### 📝 Delete a user

Finally, to delete a user, we need to pass the id in the URL.

For example, make a

```bash
DELETE request to http://localhost:8080/users/1
```

Special thanks for reference: https://dev.to/francescoxx/rust-crud-rest-api-3n45

## Contributing

Pull requests are welcome. For major changes, please open an issue first
to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License

[MIT](https://choosealicense.com/licenses/mit/)
