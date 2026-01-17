# ubuntu-devcontainer

Set up this development container remotely by creating a VS Code tunnel, connecting from your desktop, and opening the repository in a dev container with the bundled PostgreSQL instance.

## 1. Prerequisites

- Remote host running Linux with Podman or Docker available.
- VS Code Desktop with the Remote Development extension pack installed.
- VS Code CLI (`code`) installed on the remote host by following the [Developing with Remote Tunnels walkthrough](https://code.visualstudio.com/docs/remote/tunnels).
- GitHub account for authenticating the tunnel.

## 2. Start the remote tunnel

1. SSH into the remote host.
2. Run the VS Code CLI tunnel command from the directory where the CLI was unpacked:

    ```bash
    ./code tunnel --accept-server-license-terms
    ```

    Leave this terminal running; it keeps the tunnel active.

## 3. Connect from VS Code Desktop

1. On your local VS Code, press Ctrl+Shift+P (Cmd+Shift+P on macOS).
2. Run **Remote Tunnels: Connect to Tunnel...**.
3. Sign in with GitHub if prompted and pick the remote host you started in the previous step.

You now have a remote VS Code session into that machine.

## 4. Clone the repository over the tunnel

1. Open a terminal in the remote session (Terminal → New Terminal).
2. Clone and enter the repository:

    ```bash
    git clone https://github.com/worldofgeese/ubuntu-devcontainer.git
    cd ubuntu-devcontainer
    ```

## 5. Open the folder in a dev container

Follow the [Quick start: Open an existing folder in a container](https://code.visualstudio.com/docs/devcontainers/containers#_quick-start-open-an-existing-folder-in-a-container) instructions:

1. With the repository folder open in VS Code, re-run the Command Palette.
2. Choose **Dev Containers: Reopen in Container**.
3. Wait for the image build and container start to finish. The workspace mounts at `/workspaces/ubuntu-devcontainer`.

Once the build completes, you are inside the fully provisioned dev container described by this repository.

## 6. Connect to the bundled PostgreSQL

The Docker Compose stack includes a `postgres` service with username `postgres`, password `postgres`, database `postgres`, and hostname `db`.

1. In VS Code, open the PostgreSQL view and select **Add Connection**.
2. Fill in the connection dialog:
    - **Server Name**: `db`
    - **Authentication Type**: Password
    - **User Name**: `postgres`
    - **Password**: `postgres`
    - Leave **Database Name** blank to connect to the default database.
3. Expand **Advanced**, set **SSL Mode** to **Disable**, and confirm.
4. Choose **Save & Connect** to store the profile and verify the connection.

You now have a remote dev container workspace with database connectivity. Use the same tunnel workflow whenever you return—start `./code tunnel`, connect from VS Code, and reopen the folder in container mode.

