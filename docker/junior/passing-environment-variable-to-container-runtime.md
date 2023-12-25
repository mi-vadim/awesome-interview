# Demonstrate how to pass an environment variable to a container at runtime.

### Short Answer
To pass an environment variable to a Docker container at runtime, use the `-e` option with the `docker run` command, followed by the environment variable and its value. For example, `docker run -e API_KEY=12345 myapp` passes the `API_KEY` environment variable with a value of `12345` to the `myapp` container.

### Full Answer
**Step-by-Step Process:**

1. **Determine the Variable and Value**: Decide the environment variable (`VAR_NAME`) and its desired value (`value`) you want to pass to the container.

2. **Run the Container with Environment Variable**:
    - Use the `docker run` command with the `-e` option.
    - Syntax: `docker run -e "VAR_NAME=value" myimage`.
    - Example: If you're passing `API_KEY` with a value of `12345` to a container created from an image named `myapp`, use: `docker run -e "API_KEY=12345" myapp`.

3. **Verify the Environment Variable** (Optional):
    - After the container is running, you can verify the environment variable is set correctly by accessing the container's shell and echoing the variable or checking where it's utilized in your application.
    - Access the container's shell using: `docker exec -it <container_name_or_id> /bin/bash` (or `/bin/sh` for Alpine-based images).
    - Echo the variable: `echo $API_KEY`.

### Importance to Business
Passing environment variables at runtime is crucial for businesses as it allows:

- **Dynamic Configuration**: Easily adjust settings like database connections, API keys, and service endpoints without modifying the container or image, allowing for flexible deployment across different environments (development, testing, production).
- **Security**: Sensitive information like passwords or API keys can be injected at runtime rather than baked into the image, reducing the risk of exposure.

### Importance to Developer
For developers, passing environment variables at runtime:

- **Enhances Flexibility**: Easily test different configurations and settings without needing to rebuild images or make code changes.
- **Simplifies Local Development**: Quickly adjust settings to match local development environments or testing scenarios.

### Summary Table

| Aspect                | Description                                                      |
|-----------------------|------------------------------------------------------------------|
| **Command**           | `docker run -e "VAR_NAME=value" myimage`                         |
| **Use Case**          | Passing dynamic configuration or sensitive information at runtime.|
| **Business Importance** | Enables dynamic container configuration and secure handling of sensitive information. |
| **Developer Importance** | Provides flexibility and simplicity in managing application settings. |

By using environment variables with Docker containers, you're leveraging a powerful feature that enhances both the flexibility and security of containerized applications.