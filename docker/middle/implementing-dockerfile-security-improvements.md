# Implement a Dockerfile change that addresses a common security issue.

One common security issue in Docker containers is running applications as the root user, which can lead to potential security risks if the container or application is compromised. Running as root in a container is similar to running as root on a Linux machine; the process has unrestricted access, which could be exploited by attackers.

To address this issue, you can modify the Dockerfile to create a non-root user and switch to it before running the application. Here is how you can implement this change:

### Original Dockerfile (Before Security Improvement)

```Dockerfile
FROM node:14
COPY . /app
WORKDIR /app
RUN npm install
EXPOSE 3000
CMD ["node", "app.js"]
```

### Modified Dockerfile with Non-Root User

```Dockerfile
FROM node:14
# Create app directory
WORKDIR /app

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
COPY package*.json ./

RUN npm install

# Bundle app source
COPY . .

# Create a user and group with non-root privileges
RUN groupadd -r nodeuser && useradd -r -g nodeuser nodeuser

# Change the ownership of the application files to the non-root user
RUN chown -R nodeuser:nodeuser /app

# Switch to non-root user
USER nodeuser

# Your app binds to port 3000, so use the EXPOSE instruction to have it mapped by the docker daemon
EXPOSE 3000

# Define command to run the app
CMD [ "node", "app.js" ]
```

### Explanation of Changes:

1. **User Creation**: The `groupadd` and `useradd` commands create a new group and user named `nodeuser` with non-root privileges.
2. **Change Ownership**: The `chown` command updates the ownership of the application files in the `/app` directory to the `nodeuser`. This step ensures that the files have the correct permissions for the non-root user.
3. **Switch User**: The `USER` instruction changes the user context to `nodeuser`. Any RUN, CMD, or ENTRYPOINT command that follows the `USER` instruction will be executed under the specified user.

### Importance of This Change:

- **Security**: Running as a non-root user reduces the risk of a container breakout where a compromised container could gain control of the host or other containers.
- **Principle of Least Privilege**: This practice adheres to the principle of least privilege, where processes are given only the permissions necessary to perform their required tasks, reducing the scope of potential damage from an attack.
- **Compliance**: Many security standards and best practices recommend or require running services as non-root users to comply with security policies.

By implementing this change in your Dockerfile, you enhance the security posture of your containerized application, protecting it against a range of potential attacks and vulnerabilities associated with running processes as root.