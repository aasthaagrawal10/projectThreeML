# Project Three Inference Server

This repository contains the inference server for Project Three. The server uses a pre-trained model (saved as `saved_model.h5`) to classify satellite images as either `"damage"` or `"no_damage"` via HTTP endpoints and is packaged as a Docker container image built for x86 architecture.

## Container Image

The Docker container image for the inference server is hosted on Docker Hub. You can pull the image using:

```bash
docker pull aasthaagrawal10/projectthree:v1
Docker Compose
A docker-compose.yml file is provided to simplify starting and stopping the inference server container. The file maps port 5000 in the container to port 5000 on your host.

Starting the Server with Docker Compose
In the directory containing the docker-compose.yml file, run:

docker-compose up
This command will build (if necessary) and start the container, making the inference server accessible at http://localhost:5000.

Stopping the Server
To stop the running container, run:

docker-compose down
Example Requests
Once the server is running, you can test the endpoints using curl.

GET /summary
To retrieve model metadata, run:


curl http://localhost:5000/summary
Expected JSON response:


{
  "model_name": "Best Damage Classifier",
  "description": "This model classifies satellite images as damage or no_damage."
}
POST /inference
Assuming you have a test image (e.g., test_image.jpg), run:


curl --form "image=@test_image.jpg" http://localhost:5000/inference
Expected JSON response (depending on the image) will be either:


{"prediction": "damage"}
or


{"prediction": "no_damage"}
Building and Pushing the Docker Image
If you need to rebuild the Docker image, follow these steps:

Build the Docker image:
From the directory containing your Dockerfile, run:

docker build -t aasthaagrawal10/projectthree:v1 .
Log in to Docker Hub:

docker login
Push the Docker image:

docker push aasthaagrawal10/projectthree:v1
Running the Provided Grader
The course grader tests your inference server by sending requests to /summary and /inference. To test against the grader:

Start your inference server using Docker Compose:

docker-compose up
Run the grader script as per the course instructions (for example, by executing the provided start_grader.sh script).

The grader expects:

A GET request to /summary that returns a JSON object with model metadata.

A POST request to /inference that returns a JSON object with a key "prediction" whose value is either "damage" or "no_damage".

Instructions Summary:
Pull the Docker image from Docker Hub (or build it locally if needed).

Use docker-compose up to start the inference server and docker-compose down to stop it.

Use the provided example curl commands to test the server endpoints.

Run the provided grader script to verify that the server responses conform to the specification.