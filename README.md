# ssh-behind-bastion-playback

`docker-compose.yml` contains two services based on `danielguerra/alpine-sshd` Docker image with `sshd` on board:
- `bastion` service is seen **outside** of the docker-compose project network, `sshd` could be reached outside by the value of `BASTION_SSH_PORT` environment variable (equal to `4848`) contained in `.env` file;
- `internal` service could be reached by `internal` hostname **inside** the docker-compose project network, `22` port is exposed for `sshd`.

`start.sh` starts Docker Compose services and prepares `ssh-keys` volume by copying `~/.ssh/id_rsa.pub` (which correspond to `~/.ssh/id_rsa`) to the `/root/.ssh/authorized_keys`, which becomes available for both services.

`.ssh/config` could be append to `~/.ssh/config` configuration to a local machine. `ssh internal.service` should work outright.
