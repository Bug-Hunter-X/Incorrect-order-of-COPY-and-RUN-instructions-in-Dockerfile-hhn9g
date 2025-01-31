This repository demonstrates a common error in Dockerfiles: incorrect order of COPY and RUN instructions when installing Python dependencies.

The `DockerfileBug.dockerfile` shows the incorrect order, leading to the error. The `DockerfileSolution.dockerfile` shows the correct order.

The issue arises because the `RUN pip3 install -r requirements.txt` command executes *before* the `COPY requirements.txt .` command. This means the `requirements.txt` file is not present in the image's filesystem, resulting in a `FileNotFoundError`. The solution is to copy the `requirements.txt` file *before* running the installation command.