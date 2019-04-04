Example template that spins up a self-contained data science environment within a container, that includes:

1. Conda for Python dependencies
2. VSCode for full featured development
3. JupyerLab for quick protyping

Blog post goes into more detail - find it here:

https://binal.pub/2019/04/running-vscode-in-docker/

#### How to Use This All

Clone this down and rename the folder to be your project name. Modify the `environment.yml` file to include all the Python packages you need.

Say you rename the folder to `churn-prediction` - run the following:

```
cd churn-prediction
docker build -t churn-prediction .
docker run -p 8443:8443 -p 8888:8888 -v $(pwd)/data:/data -v $(pwd)/code:/code --rm -it churn-prediction
```

This will spin up the container - starting up JupyerLab and VSCode. 

VSCode will be running on:

http://localhost:8443

JupyterLab will be running on:

http://localhost:8888 with a token of `local-development`

#### VSCode Extensions and Configuration

You can install any extension and modify configuration like you would locally. Any extensions you install and global configuration you update will persist in the `./data` folder so you don't have to redo it every time you restart the container. By default VSCode will start up with the `./code` folder as the workspace, which you can change by modifying the `docker-entrypoint.sh` file.

You can pretty much VSCode as you would locally, doing things like starting up terminals, setting Python formatters/linters, and so on.

