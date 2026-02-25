* Refer to [Installation Prerequisites](../getting-started/prerequisites.md#installation-prerequisites) page for Docker-based deployment.
* <code class="expression">space.vars.SITENAME</code> supports both **Windows-based and Linux-based Docker deployments**.
  * For **Windows-based Docker deployment**, Windows Server 2019 or above is required.
    * <code class="expression">space.vars.SITENAME</code> also supports containerization for external services like ReadyOne Service and MBSE SDK Bootstrap Package service on Windows-based Docker deployment.
  * For **Linux-based Docker deployment**, ensure the supported Linux OS is installed as per Docker guidelines.
* Docker daemon should be up and running (by default, daemon comes up with Docker Desktop app). Refer [here](https://docs.docker.com/engine/install/) for the installation steps.
  * To validate the daemon running process, you can create dummy volume with the command [Docker Volume Creation](#docker-volume-creation-optional).
* Docker Compose should be installed (by default, Docker Compose comes up with Docker Desktop app). Refer [here](https://docs.docker.com/compose/install/) for the installation steps.
* Docker on Windows can run Linux-based containers. For more details around the configuration in Windows, refer to [this](https://docs.docker.com/desktop/install/windows-install/) page.