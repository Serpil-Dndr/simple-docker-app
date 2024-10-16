## Simple Docker App SetUP

1. Create a directroy 

    ```bash 
    mkdir my-docker-app
    ```

2. Navigate directory

    ```bash
    cd my-docker-app
   ```
3. Crete Jsonfile 
    ```bash
    npm init -y
    ```

4. Create app.js file 

        ```bash
        const http = require('http');

        const server = http.createServer((req, res) => {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello, Docker World!\n');
        });

        const port = process.env.PORT || 3000;
        server.listen(port, () => {
        console.log(`Server running on http://localhost:${port}`);
        });
        ```
5. Create a Dockerfile (kesinlikle root directory ile ayni seviyede olmali )

    ```bash
    # Use the official Node.js image from the Docker Hub
    FROM node:14

    # Set the working directory in the container
    WORKDIR /usr/src/app

    # Copy package.json and package-lock.json to the container
    COPY package*.json ./

    # Install application dependencies
    RUN npm install

    # Copy the rest of the application source code to the container
    COPY . .

    # Expose the port your application will run on
    EXPOSE 3000

    # Define the command to run your application
    CMD ["node", "app.js"]
    ```
6. Build the Docker image

```bash
docker build -t my-docker-app .
docker images
```
7. Run docker container 

```bash 
docker run -p 3000:3000 my-docker-app
```

8. Clean up environment 

```bash 
docker system prune -a
```