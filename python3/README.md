A minimal, and multi-architecture Python base image built on top of [Google’s base Distroless image](https://github.com/GoogleContainerTools/distroless).

The entrypoint is the Python binary, so you’ll need to set your own entrypoint to a Python file in your derived image.

### Example

```dockerfile
FROM ghcr.io/your-org/python-distroless:3.13

WORKDIR /app
COPY . .

ENTRYPOINT ["python", "main.py"]
```