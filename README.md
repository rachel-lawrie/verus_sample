# Sample Code from Verus

The following repositories contain a selection of code I wrote at Verus as one of three founding engineers. The functionality outlined here represents just a small part of a much larger codebase.

https://github.com/rachel-lawrie/verus_shared
https://github.com/rachel-lawrie/verus_backend_core



To provide context on how this code was originally structured and developed, I’ve maintained the same multi-repository setup and Docker-based environment used in the full application. This approach offers insight into both the code itself and the development environment I designed.  

While these repositories do not include the entire system, they demonstrates a piece of my contribution, coding style, and approach to building scalable software.  

## Run the app locally using Docker
First download docker desktop and make sure it is open.

### shared - monitoring, database container

Download repo: https://github.com/rachel-lawrie/verus_shared
Delete go.sum
Run `go mod tidy` to get rid of errors.

Run the following commands to start the shared services:
```bash

docker network create shared-network
docker-compose -f docker-compose-shared.dev.yml build --no-cache  
docker-compose -f docker-compose-shared.dev.yml up --remove-orphans
```
- To reload the container without rebuilding: 
```bash
docker-compose -f docker-compose.dev.yml restart app
```

**Database**
A mongodb container is launched as part of the docker set up.

To access database commands in IDE:

Run the following (in this example it is mongodb-container (replace with relevant name if needed))
```bash
docker exec -it mongodb-container mongosh -u admin -p adminpassword
```

- Identify database container name.
```bash
docker ps
```
### verus_app_backend - core platform logic, such as API endpoints that our customers would access to upload applicants, the connection to the Compliance vendors, and the business logic to provide responses.

Download repo: https://github.com/rachel-lawrie/verus_app_backend
Delete go.sum
Run `go mod tidy` to get rid of errors.

Create a .env file in the repository using the .env.example file as a template. Copy db username and password from shared/docker-compose-shared.dev.yml. Add your own AWS credentials. For the tests below, you can put a placeholder value for the webhook secret key.

Run the following to start the server:
```bash
docker-compose -f docker-compose.dev.yml build --no-cache  
docker-compose -f docker-compose.dev.yml up --remove-orphans
```



