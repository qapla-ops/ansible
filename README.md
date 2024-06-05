# Ansible Docker Image

## Overview

This Docker image is designed to provide a lightweight, consistent, and reproducible environment for running Ansible playbooks and managing configurations. It includes all the necessary dependencies and tools to streamline the process of provisioning, deploying, and orchestrating your infrastructure.

## Features

- **Pre-installed Ansible**: Comes with the latest stable version of Ansible pre-installed, ensuring you have access to the most recent features and improvements.
- **Lightweight**: Based on a minimal base image to reduce overhead and improve performance.
- **Customizable**: Easily extendable to include additional Ansible modules or custom scripts.
- **Secure**: Regularly updated to include the latest security patches and updates.
- **Versatile**: Suitable for both development and production environments, supporting a wide range of use cases from simple configuration management to complex orchestration tasks.

## Usage

### Pulling the Image

To pull the latest version of the Ansible Docker image, use the following command:

```bash
docker pull qops/ansible:latest
```

### Running Ansible Playbooks

Mount your Ansible playbooks directory and any necessary configuration files into the container, then run Ansible commands as needed:

```bash
docker run --rm \
  -v $(pwd)/playbooks:/ansible/playbooks \
  -v $(pwd)/config:/ansible/config \
  qops/ansible:latest \
  ansible-playbook /ansible/playbooks/your-playbook.yml
```

### Example

Here's a simple example to run a playbook called `site.yml` located in your current directory:

```bash
docker run --rm \
  -v $(pwd):/ansible/playbooks \
  qops/ansible:latest \
  ansible-playbook /ansible/playbooks/site.yml
```

### Extending the Image

If you need to add additional Ansible modules or other dependencies, you can create a new Dockerfile based on this image:

```dockerfile
FROM qops/ansible:latest

# Install additional packages
RUN apt-get update && apt-get install -y \
  some-package \
  && rm -rf /var/lib/apt/lists/*

# Add custom scripts or Ansible roles
COPY my-custom-scripts /usr/local/bin/

# Set working directory
WORKDIR /ansible/playbooks
```

Build and tag your custom image:

```bash
docker build -t your-custom-ansible-image .
```

## Contributing

Contributions are welcome! Please open an issue or submit a pull request on the GitHub repository if you have any suggestions or improvements.

## License

This project is licensed under the MIT License. See the LICENSE file for more details.

## Maintainers

- [Fabio Ferrari](https://github.com/qapla-fabio)

---

For more information, visit the [GitHub repository](https://github.com/qapla-ops) or the [Docker Hub page](https://hub.docker.com/r/qops/ansible).

---

This image is a part of the community-driven efforts to make Ansible accessible and easy to use in any environment. Happy automating!
