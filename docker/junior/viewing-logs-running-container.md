# Show me how to view the logs of a running container.

### Short Answer
To view the logs of a running container, use the `docker logs [CONTAINER_ID or NAME]` command. This command fetches the logs output by the container's application and displays them in your command line interface.

### Full Answer
Here's how you would typically view logs for a Docker container:

**1. Identify the Container:**
- First, identify the container you want the logs for. You can find the container ID or name using `docker ps`.
- For example, if you have a container running a web server, you might see it listed in `docker ps`.

**2. Fetching the Logs:**
- Use `docker logs [CONTAINER_ID or NAME]` to fetch and display the logs. Replace `[CONTAINER_ID or NAME]` with the actual ID or name of your container.
- For example: `docker logs my-web-container` or `docker logs f0f5be`.

**3. Additional Options:**
- **-f or --follow**: Follow log output (like `tail -f`). This is useful for watching the logs in real-time.
- **--since [TIME]**: Show logs since a certain time (e.g., `--since 1h30m` for logs in the last 1.5 hours).
- **--tail [NUMBER]**: Number of lines to show from the end of the logs (e.g., `--tail 50` shows the last 50 lines).

**Example Commands:**
- `docker logs my-web-container`: Fetches all logs from the 'my-web-container' container.
- `docker logs -f my-web-container`: Continuously follows and prints the log output.
- `docker logs --tail 100 my-web-container`: Shows the last 100 lines of the log.

### Importance to Business
Viewing logs of running containers is vital for businesses because:

- **Problem Diagnosis**: Quickly identify and diagnose issues, reducing downtime for services and applications.
- **Monitoring and Alerting**: Logs are often used to monitor container health and performance, and can trigger alerts if anomalies are detected.
- **Audit and Compliance**: Logs provide a record of activity and can be essential for audit trails and regulatory compliance.

### Importance to Developer
For developers, container logs are crucial for:

- **Debugging**: Understand what's happening inside the container, especially for issues that are not replicable outside the containerized environment.
- **Development Feedback**: Provides immediate insight into the effects of recent code changes or configurations.
- **Performance Tuning**: Helps in identifying performance bottlenecks or unexpected behavior in applications.

### Summary Table

| Aspect                  | Description                                                         |
|-------------------------|---------------------------------------------------------------------|
| **Command**             | `docker logs [CONTAINER_ID or NAME]`                                |
| **Options**             | `-f/--follow`, `--since [TIME]`, `--tail [NUMBER]`                  |
| **Business Importance** | Essential for problem diagnosis, monitoring, and compliance.         |
| **Developer Importance** | Useful for debugging, development feedback, and performance tuning.  |

The `docker logs` command is a simple yet powerful tool to help maintain oversight on the applications running within Docker containers, serving both operational and development needs effectively.