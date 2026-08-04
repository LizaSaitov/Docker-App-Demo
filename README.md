## Container App
lightweight Python Web Application containerized using Docker as part of the DevOps task requirements.

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
 
## Test the Application
Once the container is running, test it using the option below:
Browser: Open http://localhost:8080