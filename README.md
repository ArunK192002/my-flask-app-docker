# Flask PostgreSQL Docker App

This is a simple Flask web application that connects to a PostgreSQL database, all containerized using Docker and managed with Docker Compose.

## Table of Contents

- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Environment Variables](#environment-variables)
- [Database Initialization](#database-initialization)
- [Endpoints](#endpoints)
- [Troubleshooting](#troubleshooting)

## Project Structure

my-flask-app/
│
├── Dockerfile
├── docker-compose.yml
├── requirements.txt
├── app.py
├── config.py
├── models.py
└── .env


## Prerequisites

- Docker: [Install Docker](https://docs.docker.com/get-docker/)
- Docker Compose: [Install Docker Compose](https://docs.docker.com/compose/install/)

## Installation

1. Clone the repository:

   git clone https://github.com/yourusername/my-flask-app.git
   cd my-flask-app


2. Build and start the Docker containers:

   docker-compose up --build
 

## Usage

- The Flask application will be available at `http://localhost:5000`.
- Access the `/users` endpoint at `http://localhost:5000/users`.

## Environment Variables

The following environment variables are used by the application and should be set in the `.env` file:

FLASK_ENV=development
DATABASE_URL=postgresql://postgres:postgres@db/postgres

## Database Initialization

After starting the containers, you need to initialize the database:

1. Open a new terminal and execute the following command to access the running `web` container:

   docker-compose exec web flask shell

2. Inside the Flask shell, run the following commands to create the tables:

   from models import db
   db.create_all()
   exit()

## Endpoints

- **GET /**: Returns a "Hello, World!" message.
- **GET /users**: Returns a list of users in JSON format.

## Troubleshooting

### Common Issues

- **ModuleNotFoundError**: Ensure all dependencies are listed in `requirements.txt` and rebuild the Docker image.
- **Database Connection**: Verify the `DATABASE_URL` in the `.env` file is correctly configured.

### Checking Logs

Check the logs for the `web` and `db` services using:

docker-compose logs web
docker-compose logs db

### Container Status

Ensure all containers are running without issues:

docker-compose ps

### Adding a User via Flask Shell

1. Open a new terminal and execute the following command to access the running `web` container:

   docker-compose exec web flask shell

2. Inside the Flask shell, run the following commands to add a new user:

   from models import db, User
   new_user = User(name='John Doe', email='john@example.com')
   db.session.add(new_user)
   db.session.commit()
   exit()

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Flask: [Flask Documentation](https://flask.palletsprojects.com/)
- Docker: [Docker Documentation](https://docs.docker.com/)
- PostgreSQL: [PostgreSQL Documentation](https://www.postgresql.org/docs/)
```

This `README.md` file provides a clear and structured overview of your project, guiding users through the installation, usage, and troubleshooting steps.
