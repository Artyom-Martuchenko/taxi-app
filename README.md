# TAXI-APP

# START PROJECT FOR TESTING(FULLY DOCKERIZED):

NOTE THAT client/cypress.json should point to dockerized client through dockerized nginx: "baseUrl": "http://localhost:8080" NOTE THAT taxi-server in docker-compose.local.yml should point to test.env file for testing with cypress

~$ git clone https://github.com/Artyom-Martuchenko/taxi-app.git

~$ cd taxi-app

~/taxi-app$ sudo docker-compose -f docker-compose.local.yml up --build

~/taxi-app$ sudo docker-compose -f docker-compose.local.yml exec taxi-server python manage.py migrate

~/taxi-app$ sudo docker-compose -f docker-compose.local.yml exec taxi-server python manage.py test trips.tests

~/taxi-app$ cd client/

~/taxi-app/client$ npx cypress open

check if db tables exists:

~/taxi-app$ sudo docker-compose -f docker-compose.local.yml exec taxi-database psql -U taxi

# START PROJECT FOR DEVELOPMENT( with dockerized postgres and dockerized redis ):

NOTE THAT client/cypress.json should point to NOT dockerized client: "baseUrl": "http://localhost:3000" NOTE THAT taxi-server in docker-compose.local.yml should point to test.env file for testing with cypress

~$ git clone https://github.com/Artyom-Martuchenko/taxi-app.git

~$ cd taxi-app

~/taxi-app$ sudo docker-compose -f docker-compose.postgres.redis.yml up

~/taxi-app/server$ python taxi/manage.py migrate

~/taxi-app/server$ python taxi/manage.py runserver

~/taxi-app/client$ npm start

~/taxi-app/client$ npx cypress open

# SOME NOTES:

To reset the database, start by running the following command in your terminal, while your Docker containers are running:
$ docker-compose exec taxi-database psql -U taxi -d test
Then run the following command to delete the users and their related data:
TRUNCATE trips_user CASCADE;

~/taxi-app$ sudo docker-compose -f docker-compose.local.yml exec taxi-server python taxi/manage.py createsuperuser

RUNNING THE POSTGRES DATABASE LOCALLY ON DOCKER (EXAMPLE 1)
Install docker image postgres:11

Start a docker container with that postgres image. $ sudo docker run --rm --name pg-docker -e POSTGRES_PASSWORD=docker -e POSTGRES_DB=somebase -e POSTGRES_USER=docker -p 5432:5432 -v $home/docker/volumes/postgres:/var/lib/postgresql/data postgres:11

Create a databe with name 'everycheese' in potgresql $ createdb -h localhost --username=docker everycheese

SET env variable directly to the system: $ export DATABASE_URL=postgres://docker:docker@127.0.0.1:5432/everycheese

$ pip install -r requirements.txt

$ python manage.py migrate

RUNNING THE POSTGRES DATABASE LOCALLY ON DOCKER (EXAMPLE 2)
Run docker-compose to up postgres and redis:

$ sudo docker-compose -f docker-compose.postgres.redis.yml up --build

Connect to PostgreSQL container to check if it works:

$ psql -h localhost -p 5432 -d docker -U docker --password
