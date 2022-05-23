ARG VARIANT="6.0"
FROM mcr.microsoft.com/vscode/devcontainers/dotnet:0-${VARIANT}

# [Option] Install Node.js
ARG INSTALL_NODE="false"

# [Option] Install Azure CLI
ARG INSTALL_AZURE_CLI="false"

# Install additional OS packages.
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends postgresql-client-common postgresql-client

# Run the remaining commands as the "vscode" user
USER vscode

# Install EF and code generator development tools
RUN dotnet tool install --global dotnet-ef
RUN dotnet tool install --global dotnet-aspnet-codegenerator
RUN echo 'export PATH="$PATH:/home/vscode/.dotnet/tools"' >> /home/vscode/.bashrc

WORKDIR /app

# Prevent the container from closing automatically
ENTRYPOINT ["tail", "-f", "/dev/null"]
