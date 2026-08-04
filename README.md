## Container App
Lightweight Python Web Application containerized using Docker.
It serves HTTP requests on port 8080 and returns a response message whenever accessed.

## Project Overview
Project objectives:
* Create a git repository
* Create a python app that listens on a port and prints a message.
* Create a docker image and conatiner


## Project Structure
```bash
.
├── app.py           # Main Flask web application
├── Dockerfile       # Container build instructions
├── requirements.txt # Project Python dependencies
└── README.md        # Project documentation
```

## Prerequisites
- Python 3.14.4
- Docker Installed and running

## Local Setup
1. Install dependencies locally:
   ```bash
   pip install -r requirements.txt
   ```
2. Build the Docker Image
   ```bash
   docker build -t docker_app . 
   ```
3. Run the Container
   ```bash
   docker run -p 8080:8080 docker_app 
   ```
4. Test the Application:
   ```
   Once the container is running, test it using the option below:
   Browser: Open http://localhost:8080
   ```