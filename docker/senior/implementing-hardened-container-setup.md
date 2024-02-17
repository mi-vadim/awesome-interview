Implementing a hardened container setup for a sensitive application involves applying security best practices and leveraging Docker's advanced security features to minimize vulnerabilities and protect against threats. This solution outlines a strategy for hardening Docker containers, focusing on configuration, network security, access control, and monitoring.

### 1. Use Official, Minimal Base Images

- **Action**: Start with minimal, official base images from trusted sources (e.g., Alpine Linux) to reduce the attack surface.
- **Benefit**: Minimizes the number of packages and potential vulnerabilities.

### 2. Implement Docker Content Trust (DCT)

- **Action**: Enable Docker Content Trust to ensure that only signed images are used in your environment.
- **Benefit**: Prevents the use of unauthorized or tampered images.

### 3. Non-Root User

- **Action**: Configure containers to run as a non-root user whenever possible.
- **Benefit**: Limits the potential impact of container compromise.

### 4. Filesystem & Volumes

- **Action**: Mount volumes as read-only and use Docker's `--tmpfs` flag for temporary data.
- **Benefit**: Prevents unauthorized data persistence and tampering.

### 5. Network Configuration

- **Action**: Use Docker's user-defined networks to isolate container communication and leverage built-in encryption for Swarm networks.
- **Benefit**: Enhances network security and isolates application components.

### 6. Limit Resources

- **Action**: Use Docker's resource limits (CPU, memory, and disk I/O) to prevent Denial of Service (DoS) attacks.
- **Benefit**: Protects the host system and other containers from resource exhaustion.

### 7. Secure Computing Mode (Seccomp)

- **Action**: Apply a custom Seccomp profile that only allows necessary system calls.
- **Benefit**: Reduces the risk of kernel exploits and privilege escalation.

### 8. Update and Scan Regularly

- **Action**: Regularly update the Docker engine, host system, and container images. Use tools like Docker Scan to detect vulnerabilities.
- **Benefit**: Ensures protection against known vulnerabilities and threats.

### 9. Implement Logging and Monitoring

- **Action**: Use Docker's logging drivers to collect container logs. Integrate with a centralized logging solution for monitoring and alerting.
- **Benefit**: Enables real-time detection of suspicious activities and operational issues.

### 10. Use Docker Bench for Security

- **Action**: Run Docker Bench for Security to audit the host and Docker daemon against common best practices.
- **Benefit**: Identifies configuration issues and areas for improvement.

### Example Hardened Dockerfile for a Web Application

```Dockerfile
# Use an official, minimal base image
FROM alpine:3.12

# Install only the necessary packages
RUN apk add --no-cache nginx

# Create a non-root user and switch to it
RUN adduser -D -g 'www' www
USER www

# Copy the web application files
COPY --chown=www:www ./webapp /var/www

# Configure Nginx to run on a non-standard port to avoid needing root
EXPOSE 8080
CMD ["nginx", "-g", "daemon off;"]
```

### Security Policy Example

Implement a security policy that enforces:
- Regular vulnerability scanning and updates.
- Use of custom Seccomp profiles for all deployed containers.
- Network segmentation and firewall rules to restrict access to containers.

### Conclusion

This hardened container setup focuses on minimizing the attack surface, enforcing principle of least privilege, isolating components, and maintaining vigilance through monitoring and regular updates. By implementing these practices, you can significantly enhance the security posture of containers running sensitive applications, protecting them against unauthorized access and exploitation.