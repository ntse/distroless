A minimal, and multi-architecture Python base image built on top of [Google’s base Distroless image](https://github.com/GoogleContainerTools/distroless).

The entrypoint is the Python binary, so you’ll need to set your own entrypoint to a Python file in your derived image.

### Example

```dockerfile
FROM ghcr.io/ntse/distroless/python:3.10

WORKDIR /app
COPY . .

ENTRYPOINT ["python", "main.py"]
```

### Images available

| Image | Tags |
|-------|------|
| ghcr.io/ntse/distroless/python | 3.10, 3.11, 3.12, 3.12 |
