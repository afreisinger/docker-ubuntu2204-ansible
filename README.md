# Ubuntu 22.04 LTS (Jammy Jellyfish) Ansible Test Image

[![Build](https://github.com/afreisinger/docker-ubuntu2204-ansible/actions/workflows/build.yml/badge.svg)](https://github.com/afreisinger/docker-ubuntu2204-ansible/actions/workflows/build.yml) [![Docker pulls](https://img.shields.io/docker/pulls/afreisinger/docker-ubuntu2204-ansible)](https://hub.docker.com/r/afreisinger/docker-ubuntu2204-ansible/)

Ubuntu 22.04 LTS (Jammy Jellyfish) Docker container for Ansible playbook and role testing.

## Tags

  - `latest`: Latest stable version of Ansible.

The latest tag is a lightweight image for basic validation of Ansible playbooks.

## How to Build

This image is built on Docker Hub automatically any time the upstream OS container is rebuilt, and any time a commit is made or merged to the `main` branch. But if you need to build the image on your own locally, do the following:

  1. [Install Docker](https://docs.docker.com/install/).
  2. `cd` into this directory.
  3. Run `docker build -t ubuntu2204-ansible .`

## How to Use

  1. [Install Docker](https://docs.docker.com/engine/installation/).
  2. Pull this image from Docker Hub: `docker pull afreisinger/docker-ubuntu2204-ansible:latest` (or use the image you built earlier, e.g. `ubuntu2204-ansible:latest`).
  3. Run a container from the image: `docker run --detach --privileged --volume=/sys/fs/cgroup:/sys/fs/cgroup:rw --cgroupns=host geerlingguy/docker-ubuntu2204-ansible:latest` (to test my Ansible roles, I add in a volume mounted from the current working directory with ``--volume=`pwd`:/etc/ansible/roles/role_under_test:ro``).
  4. Use Ansible inside the container:
    a. `docker exec --tty [container_id] env TERM=xterm ansible --version`
    b. `docker exec --tty [container_id] env TERM=xterm ansible-playbook /path/to/ansible/playbook.yml --syntax-check`

## Notes

I use Docker to test my Ansible roles and playbooks on multiple OSes using CI tools like Jenkins and Travis. This container allows me to test roles and playbooks using Ansible running locally inside the container.

> **Important Note**: I use this image for testing in an isolated environment—not for production—and the settings and configuration used may not be suitable for a secure and performant production environment. Use on production servers/in the wild at your own risk!

## Author

Created in 2025 by [Adrian Freisinger](https://afreisinger.gitlab.io/), inspired by [Ansible for DevOps](https://www.ansiblefordevops.com/) by [Jeff Geerling](https://www.jeffgeerling.com/).
