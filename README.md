# Containerize a web server

## Plan

### Phase 1: Create the web server

1. We want to build a simple web server in Flask.
2. We want to use `uv` to manage Python virtual environments and dependencies.
3. We want to run the web server locally.

### Phase 2: Build the image locally

1. We want to create a Dockerfile to build the web server into an image.
2. Build the image for multiple architectures (arm64 and amd64).
3. Manually push the image to DockerHub

### Phase 3: Build the image via pipeline

1. Create a GitHub Actions workflow.
2. Build the image for multiple architectures (arm64 and amd64).
3. Run a test to check the image for security vulnerabilities.
4. Push the image to DockerHub.

## Getting started

### Prerequisites

- Python 3.14+
- [uv](https://docs.astral.sh/uv/)
- Docker (with buildx support)

Verify your environment:

```bash
python3 --version     # Should be 3.14 or higher
uv --version          # Should show uv version
docker --version      # Should show Docker version
docker buildx version # Should show buildx version
```

### Run the web server locally

```bash
# Install dependencies
uv sync

# Start the server
uv run python src/app.py
```

The server starts on `http://localhost:5050`.

- `GET /` — Welcome message
- `GET /hello?name=Jon` — Responds with "Hello, Jon."
- `GET /hello` — Defaults to "Hello, World."

### Build the image locally

Replace `<your-dockerhub-username>` with your DockerHub username.

```bash
docker buildx build --platform linux/amd64,linux/arm64 \
  -t <your-dockerhub-username>/my-first-web-server:latest .
```


