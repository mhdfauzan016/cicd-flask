# Welcome App

A simple web application that displays welcome messages based on the provided name.

## Overview

This repository contains a simple Flask web application that responds to requests at the `/welcome/{name}` endpoint. If a name is provided, it displays "Selamat datang {name}". If no name is provided, it displays "Selamat datang Anonymous".

## Repository Structure

```
welcome-app/
├── app.py                  # Flask application code
├── Dockerfile              # Docker image definition
├── docker-compose.yaml     # Docker Compose configuration
├── kubernetes/             # Kubernetes deployment manifests
│   ├── configmap.yaml
│   ├── secret.yaml
│   ├── deployment.yaml
│   ├── service.yaml
│   └── ingress.yaml
└── .github/workflows/      # GitHub Actions workflow files
    └── docker-build-deploy.yml
```

## Getting Started

### Prerequisites

- Docker and Docker Compose
- Kubernetes cluster (for Kubernetes deployment)
- GitHub account (for CI/CD)

### Local Development

1. Clone the repository:
   ```bash
   git clone https://github.com/mhdfauzan016/cicd-flask.git
   cd welcome-app
   ```

2. Run the application directly:
   ```bash
   pip install flask
   python app.py
   ```

3. Access the application:
   - http://localhost:5000/welcome/YourName
   - http://localhost:5000/welcome/

## Deployment Options

### Docker Deployment

Build and run using Docker:

```bash
# Build the image
docker build -t testing/welcome .

# Run the container
docker run -d -p 8000:5000 testing/welcome
```

Access the application at:
- http://localhost:8000/welcome/YourName
- http://localhost:8000/welcome/

### Docker Compose Deployment

Deploy using Docker Compose:

```bash
# Start the service
docker-compose up -d

# Stop the service
docker-compose down
```

Access the application at:
- http://localhost:8000/welcome/YourName
- http://localhost:8000/welcome/

### Kubernetes Deployment

Deploy to a Kubernetes cluster:

```bash
# Apply all Kubernetes manifests
kubectl apply -f kubernetes/

# Or apply individual components
kubectl apply -f kubernetes/configmap.yaml
kubectl apply -f kubernetes/secret.yaml
kubectl apply -f kubernetes/deployment.yaml
kubectl apply -f kubernetes/service.yaml
kubectl apply -f kubernetes/ingress.yaml
```

Access via the configured Ingress or use port forwarding:
```bash
kubectl port-forward svc/welcome-app-service 8080:80
```

Then access at http://localhost:8080/welcome/YourName

## CI/CD Pipeline

This repository includes GitHub Actions workflows for continuous integration and deployment.

### Setup

1. Configure the following secrets in your GitHub repository:
   - `DOCKER_HUB_USERNAME`: Your Docker Hub username
   - `DOCKER_HUB_TOKEN`: Your Docker Hub access token
   - `SSH_PRIVATE_KEY`: (Optional) For VM deployment

2. The workflow will:
   - Build the Docker image
   - Push to Docker Hub with tags:
     - `testing/welcome:latest`
     - `testing/welcome:x.x.x` (version tag)
   - Create a GitHub release
   - Deploy to VM (if configured)

3. Trigger the workflow:
   - Go to the Actions tab in GitHub
   - Select the workflow
   - Click "Run workflow"
   - Provide the branch, version tag, and other required inputs

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.