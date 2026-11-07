# Cloud Service Demo

## Purpose

This project is a small example of a web page that could be deployed as a cloud-hosted service. It demonstrates a simple homepage and a benefit of cloud computing.

## Files

- `README.md` — describes the project and its files.
- `index.html` — the demo homepage.

Version control helps a cloud project by recording changes, making it easier to collaborate, review updates, and restore an earlier version when needed.

## Running with Docker

Docker is a platform for packaging and running applications in isolated environments. A Docker image is a packaged template containing an application and what it needs to run. A Docker container is a running instance of an image.

Build the image from this project, then start a container and access the homepage at `http://localhost:8080`:

```sh
docker build -t cloud-service-demo:1.0 .
docker run -d --name cloud-demo-container -p 8080:80 cloud-service-demo:1.0
```