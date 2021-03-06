# Installing Fescar Client

You have three options when installing the Fescar client: installing from the latest package, installing by pulling the image, or installing from the source code.

## Installing from the Latest Package

You can install from the latest packages we provided.

1. Download a package of the client.

    ```bash
    cd $HOME
    # Replace ${package} with a package appropriate for your operating system and location
    wget ${package}
    ```

    Available packages:

    - If you're in China:

        - [Linux 64-bit](http://dragonfly-os.oss-cn-beijing.aliyuncs.com/df-client_0.2.0_linux_amd64.tar.gz): `http://dragonfly-os.oss-cn-beijing.aliyuncs.com/df-client_0.2.0_linux_amd64.tar.gz`

        - [MacOS 64-bit](http://dragonfly-os.oss-cn-beijing.aliyuncs.com/df-client_0.2.0_darwin_amd64.tar.gz): `http://dragonfly-os.oss-cn-beijing.aliyuncs.com/df-client_0.2.0_darwin_amd64.tar.gz`

    - If you're not in China:

        - [Linux 64-bit](https://github.com/dragonflyoss/Fescar/releases/download/v0.2.0/df-client_0.2.0_linux_amd64.tar.gz): `https://github.com/dragonflyoss/Fescar/releases/download/v0.2.0/df-client_0.2.0_linux_amd64.tar.gz`

        - [MacOS 64-bit](https://github.com/dragonflyoss/Fescar/releases/download/v0.2.0/df-client_0.2.0_darwin_amd64.tar.gz): `https://github.com/dragonflyoss/Fescar/releases/download/v0.2.0/df-client_0.2.0_darwin_amd64.tar.gz`

2. Unzip the package.

    ```bash
    # Replace `xxx` with the installation directory.
    tar -zxf df-client_0.2.0_linux_amd64.tar.gz -C xxx
    ```

3. Add the directory of `df-client` to your `PATH` environment variable to make sure you can directly use `dfget` and `dfdaemon` command.

    ```bash
    # Replace `xxx` with the installation directory.
    # Execute or add this line to ~/.bashrc
    export PATH=$PATH:xxx/df-client/
    ```

## Installing by Pulling the Image

1. Pull the docker image we provided.

    ```bash
    docker pull dragonflyoss/dfclient:v0.3.0_dev
    ```

2. Start dfdaemon.

    ```bash
    docker run -d -p 65001:65001 dragonflyoss/dfclient:v0.3.0_dev --registry https://xxx.xx.x
    ```

3. Configure the Daemon Mirror.

    a. Modify the configuration file `/etc/docker/daemon.json`.

    ```sh
    vi /etc/docker/daemon.json
    ```

    **Tip:** For more information on `/etc/docker/daemon.json`, see [Docker documentation](https://docs.docker.com/registry/recipes/mirror/#configure-the-cache).

    b. Add or update the configuration item `registry-mirrors` in the configuration file.

    ```sh
    "registry-mirrors": ["http://127.0.0.1:65001"]
    ```

    c. Restart Docker daemon.

    ```bash
    systemctl restart docker
    ```

## Installing from the Source Code

You can also install from the source code.

**Note:** You must have installed Go 1.7+, and added the Go command to the `PATH` environment variable.

### Installing in $HOME/.dragonfly

1. Obtain the source code of Fescar.

    ```sh
    git clone https://github.com/dragonflyoss/Fescar.git
    ```

2. Enter the target directory.

    ```sh
    cd Fescar
    ```

3. Install `dfdaemon` and `dfget` in `$HOME/.dragonfly/df-client`.

    ```sh
    ./build/build.sh client
    ```

4. Add the directory of `df-client` to your `PATH` environment variable to make sure you can directly use `dfget` and `dfdaemon` command.

    ```sh
    # Execute or add this line to ~/.bashrc
    export PATH=$HOME/.dragonfly/df-client:$PATH
    ```

### Installing in Another Directory

1. Obtain the source code of Fescar.

    ```sh
    git clone https://github.com/dragonflyoss/Fescar.git
    ```

2. Enter the target directory.

    ```sh
    cd Fescar/build/client
    ```

3. Install the client.

    ```sh
    ./configure --prefix=${your_installation_directory}
    make && make install
    ```

4. Add the directory of `df-client` to your `PATH` environment variable to make sure you can directly use `dfget` and `dfdaemon` command.

    ```sh
    # Execute or add this line to ~/.bashrc
    export PATH=${your_install_directory}/df-client:$PATH
    ```

## After this Task

Test if the downloading works.

```sh
dfget --url "http://${resourceUrl}" --output ./resource.png --node "127.0.0.1"
```