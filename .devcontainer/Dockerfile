# Template Repository:
# - https://github.com/devcontainers/templates/tree/template_go-postgres_1.2.2/src/python
# - https://github.com/microsoft/vscode-dev-containers/tree/v0.245.2/containers/python-3
#   - Most of the contents of this repository have been migrated to the above repository.

# Get a image.
# - https://mcr.microsoft.com/v2/devcontainers/python/tags/list
# - https://mcr.microsoft.com/v2/vscode/devcontainers/python/tags/list
ARG IMAGE_VERSION="0"           # x, x.x, x.x.x
ARG PYTHON_VERSION="3"          # x, x.x
ARG DEBIAN_VERSION="bullseye"   # bullseye: Debian 11, buster: Debian 10
# FROM mcr.microsoft.com/devcontainers/python:${IMAGE_VERSION}-${PYTHON_VERSION}-${DEBIAN_VERSION}
FROM mcr.microsoft.com/vscode/devcontainers/python:${IMAGE_VERSION}-${PYTHON_VERSION}-${DEBIAN_VERSION}

# Install packages.
RUN apt update && export DEBIAN_FRONTEND=noninteractive && apt -y install --no-install-recommends iputils-ping
RUN apt update && export DEBIAN_FRONTEND=noninteractive && apt -y install --no-install-recommends dnsutils
RUN apt update && export DEBIAN_FRONTEND=noninteractive && apt -y install --no-install-recommends task-japanese

# Config python.
RUN python -m pip install --upgrade pip
RUN pipx install poetry
RUN poetry config virtualenvs.in-project true

# Add a proc to export envs.
RUN echo "" >> ~/.bashrc && \
    echo "# Display time in the bash_histroy." >> ~/.bashrc && \
    echo "export HISTTIMEFORMAT='[%Y/%m/%d %H:%M:%S %Z] '" >> ~/.bashrc

# Add a proc to read the alias definition file.
RUN echo "" >> ~/.bashrc && \
    echo "# Read the alias definition file." >> ~/.bashrc && \
    echo "if [ -f ~/.bash_aliases ]; then" >> ~/.bashrc && \
    echo "    . ~/.bash_aliases" >> ~/.bashrc && \
    echo "fi" >> ~/.bashrc

# Set a language and a territory.
RUN sed -i -E 's/# (ja_JP.UTF-8)/\1/' /etc/locale.gen
RUN locale-gen
ENV LANG ja_JP.UTF-8

# Set a timezone.
RUN ln -sf /usr/share/zoneinfo/Japan /etc/localtime
