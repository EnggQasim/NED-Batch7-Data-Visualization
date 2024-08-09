To set up a Jupyter Notebook environment using Docker Compose with a Dockerfile, you can follow the steps below:

### 1. **Create a Directory for Your Project**
   First, create a directory for your project.

   ```bash
   mkdir jupyter-notebook-setup
   cd jupyter-notebook-setup
   ```

### 2. **Create a `Dockerfile`**
   Create a `Dockerfile` inside the project directory. This file will define the environment.

   ```Dockerfile
   # Dockerfile

   # Use the official Jupyter Notebook base image
   FROM jupyter/base-notebook:latest

   # Set environment variables for Jupyter
   ENV JUPYTER_ENABLE_LAB=yes

   # Expose the default Jupyter port
   EXPOSE 8888

   # Optionally, install additional Python packages
   RUN pip install --no-cache-dir \
       numpy \
       pandas \
       matplotlib \
       scikit-learn

   # Set the command to start Jupyter Notebook
   CMD ["start-notebook.sh"]
   ```

   This `Dockerfile` starts from a base image that includes Jupyter Notebook and allows you to install additional Python packages.

### 3. **Create a `docker-compose.yml` File**
   Create a `docker-compose.yml` file in the same directory to define the services and how they interact.

   ```yaml
   version: '3.8'

   services:
     jupyter:
       build: .
       ports:
         - "8888:8888"
       volumes:
         - ./notebooks:/home/jovyan/work
       environment:
         - JUPYTER_TOKEN=mysecuretoken
   ```

   - **build**: Specifies that Docker Compose should build the image using the Dockerfile in the current directory (`.`).
   - **ports**: Maps port 8888 on your local machine to port 8888 in the container.
   - **volumes**: Mounts the `notebooks` directory from your host to the Jupyter working directory inside the container. This ensures that your notebooks are stored on your local machine.
   - **environment**: Sets an environment variable to secure Jupyter Notebook with a token. You can replace `mysecuretoken` with a more secure token or password.

### 4. **Create a Directory for Notebooks**
   Create a directory where your Jupyter notebooks will be stored.

   ```bash
   mkdir notebooks
   ```

### 5. **Build and Run the Docker Container**
   Now, build the Docker image and start the container with Docker Compose.

   ```bash
   docker-compose up --build
   ```

   This command will build the Docker image and start the Jupyter Notebook server.

### 6. **Access Jupyter Notebook**
   Once the container is running, open your web browser and navigate to:

   ```
   http://localhost:8888/?token=mysecuretoken
   ```

   Replace `mysecuretoken` with the token you set in the `docker-compose.yml` file.

### 7. **Stop the Container**
   When you're done, you can stop the Jupyter Notebook container with:

   ```bash
   docker-compose down
   ```

This setup provides a reusable, isolated Jupyter Notebook environment that can be easily shared and deployed.