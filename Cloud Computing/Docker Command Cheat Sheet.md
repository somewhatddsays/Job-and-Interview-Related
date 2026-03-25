# Docker Command &mdash; Cheat Sheet For Data Scientist


### 1. Docker Basics (Foundation Layer)

Understand what Docker is doing before using commands.

| Command            | Description                                                                                                                              |
|:-------------------|:-----------------------------------------------------------------------------------------------------------------------------------------|
| `docker --version` | Confirms Docker installation and version compatibility, especially important for **GPU** and **ML** frameworks.                          |
| `docker info`      | Dispplays system-level details like number of containers, images, storage driver, and **runtime environment.** Helps debug setup issues. |
| `docker help`      | Lists all available commands and subcommands. Useful when exploring new Docker features or forgetting syntax.                            |

> Think of Docker as a lightweight virtual machine optimized for running isolated data science environments.

 --- 



### 2. 

Images define your Python, libraries, and dependencies.

| Command                  | Description                                                                                                |
|:-------------------------|:-----------------------------------------------------------------------------------------------------------|
| `docker pull <image>`    | Downloads a pre-built environment (e.g., python:3.10, pytorch). Ensures consistency across machines.       |
| `docker image`           | Lists all locally available images with size, version tags, and ID's &mdash; helpful for managing storage. |
| `docker rmi <image_id>`  | Removes unused images to free space, especially important when working with large `ML Images`.             |
| `docker build -t <name>` | Builds a custom image using a Dockerfile (e.g., installing `pandas`, `scikit-learn`, `TensorFlow`) .       |


> Images are immutable &mdash; once built, they don't change. This guarantees reproducibility in ML workflows.


 --- 



### 3. Running Containers (Execution Layer)

Containers are live instances of your ML Environment.

| Command                                  | Description                                                                                         |
|:-----------------------------------------|:----------------------------------------------------------------------------------------------------|
| `docker run <image>`                     | Starts a container from an image. Equivalent to launching a new isolated environment.               |
| `docker run -it <image>` bash            | Opens an interactive terminal to run Python scripts, debug code, or install packages manually.      |
| `docker run -d <image>`                  | Runs container in detached mode (background), useful for APIs or model-serving systems.             |
| `docker run --name my_container <image>` | Assigns a readable name for easier management instead of random container IDs.                      |
| `docker run -p 8888:8888 <image>`        | Maps container ports to local machine commonly used for Jupyter Notebook, Streamlit, or Dashboards. |

> Every container is isolated no dependency conflicts like "different pandas version broke my code".



 --- 



### 4. Managing Containers (Control Layer)

Handles running experiments and workflows efficiently.

| Command                       | Description                                                                                    |
|:------------------------------|:-----------------------------------------------------------------------------------------------|
| `docker ps`                   | Shows currently running containers along with status, ports, and names.                        |
| `docker ps -a`                | Lists all containers, including stopped ones &mdash; useful for tracking previous experiments. |
| `docker stop <container_id>`  | Gracefully stops a running container without deleting it.                                      |
| `docker start <container_id>` | Restarting a previously stopped container with the same state.                                 |
| `docker rm <container_id>`    | Permanently removes a container to clean up unused resources.                                  |

> Containers are temporary by design &mdash; treat them as disposable compute environments.


 --- 



### 5. 

Ensure datasets and models are not lost.

| Command                                 | Description                                                                           |
|:----------------------------------------|:--------------------------------------------------------------------------------------|
| `docker volume create my_volume`        | Createse a persistent storage independent of containers.                              |
| `docker volume ls`                      | Lists all volumes, helping you track stored datasets or model artifacts.              |
| `docker run -v my_volume:/app <images>` | Mount volume inside container, allowing persistent access to files.                   |
| `docker run -v $(pwd):/app <images>`    | Links your local project directory to the container, enabling real-time code updates. |

> Without volumes, all your trained models and data disappear when the container stops.

 --- 



### 6. Working with Files (Data Movement Layer)

Move data between local system and container

| Command                                | Description                                                                            |
|:---------------------------------------|:---------------------------------------------------------------------------------------|
| `docker cp file.txt <container>:/path` | Transfers dataset, scripts, or configs into the container.                             |
| `docker cp <container>:/path file.txt` | Extracts results like trained models, logs, or outputs from container to local system. |

> Useful when working with batch ML jobs or exporting trained models.

 --- 



### 7. Logs & Debugging (Monitoring Layer)

Debug ML Pipelines and errors inside containers

| Command                               | Description                                                                      |
|:--------------------------------------|:---------------------------------------------------------------------------------|
| `docker logs <container_id>`          | Displaying output logs, useful for tracking training progress or runtime errors. |
| `docker exec -it <container_id> bash` | Enters a running container to inspect files, debug scripts, or test fixes.       |
| `docker inspect <container_id>`       | Provides deep details (IP, configs, mounts, environment variables).              |

Essential when your model fails silently or behaves differently in production.

 --- 



### 8. Networking (Pipeline Connectivity Layer)
Connect multiple services like ML Model + Database

| Command                                   | Description                                                    |
|:------------------------------------------|:---------------------------------------------------------------|
| `docker network ls`                       | Lists all available networks.                                  |
| `docker network create my_network`        | Creates a custom network for communication between containers. |
| `docker run --network my_network <image>` | Connects container to a specific network.                      |

> Used when building systems like: Model API + PostgreSQL + Redis cache

 --- 



### 9. Docker Compose (Orchestration Layer)

Run complete ML Pipeline with multiple services

| Command                | Description                                              |
|:-----------------------|:---------------------------------------------------------|
| `docker-compose up`    | Starts all services defined in docker-compose.yml        |
| `docker-compose down`  | Stops and removes all services.                          |
| `docker-compose build` | Builds images for all services defined in configuration. |

> Perfect for end-to-end pipelines: 
> `data ingestion` &Rarr; `processing` &Rarr; `model`  &Rarr; `API`

 --- 

### 10. GPU Support (Deep Learning Layer)

Enable hardware acceleration for training models.

`docker run --gpus all <images>` **&rarr;** Allows container to use GPU resources.<>

**Example**
```aiignore
docker run --gpus all tensorflow/tensorflow:latest-gpu
```

 --- 



