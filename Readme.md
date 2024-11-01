
# NSIS Docker Container

This Docker container is built using Debian and provides an environment to run NSIS (Nullsoft Scriptable Install System) commands with a specified verbosity level.

## Prerequisites

Make sure you have Docker installed on your system before building and running this container.

## Building the Docker Image

Use the following command to build the Docker image. Replace `<image-name>` with your preferred name for the image.

```bash
docker build -t <image-name> .
```

## Running the Docker Container

After building the image, you can run NSIS commands by using the Docker container. Here's an example of how to do that:

```bash
docker run --rm -v $(pwd):/app <image-name> /app/your-script.nsi
```

In this example:
- The `--rm` flag removes the container after it finishes running.
- The `-v $(pwd):/app` flag mounts the current directory to `/app` inside the container, so NSIS can access your scripts and files.
- Replace `<image-name>` with the name you used when building the Docker image.
- Replace `your-script.nsi` with the path to your NSIS script.

### Example: Custom NSIS Arguments

If you need to pass additional arguments to NSIS, simply add them after specifying the script path:

```bash
docker run --rm -v $(pwd):/app <image-name> /app/your-script.nsi /DOUTDIR=/app/output
```

This will pass `/DOUTDIR=/app/output` to the NSIS script.

## Environment Variables

The container has the following environment variables set:
- `NSIS=3.10-2`: Specifies the NSIS version to install.
- `VERBOSITY=4`: Sets the NSIS verbosity level (adjust as needed).

### Modifying Verbosity

To modify the verbosity level, you can change the `VERBOSITY` environment variable in the Dockerfile or override it at runtime:

```bash
docker run --rm -v $(pwd):/app -e VERBOSITY=2 <image-name> /app/your-script.nsi
```