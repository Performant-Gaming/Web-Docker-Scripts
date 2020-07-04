# Notes
## Building Image
You may use the following command to build this image:

```
docker build -t pg:latest .
```

## Running Container
I use the following command to run the container:

```
docker run -d -v /path/to/containers/pg:/var/pg/ --name pg --restart unless-stopped -p 4568:4567 pg
```

**Note** - We expose port `4568` to the host and it maps to `4567` which is what NodeBB listens on inside the container.

After running, you can start, stop, and restart the container with the following commands:

```
docker stop pg      # Stops PG container.
docker start pg     # Starts PG container.
docker restart pg   # Restarts PG container.
```