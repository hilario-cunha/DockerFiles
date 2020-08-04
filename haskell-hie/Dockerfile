FROM haskell:8.8.3

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Create the user
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    #
    # [Optional] Add sudo support. Omit if you don't need to install software after connecting.
    && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME \
    && mkdir -p /etc/stack \
    && cp /root/.stack/config.yaml /etc/stack/config.yaml \
    && chmod 0644 /etc/stack/config.yaml
# ********************************************************
# * Anything else you want to do like clean up goes here *
# ********************************************************

# [Optional] Set the default user. Omit if you want to keep the default as root.
USER $USERNAME

# Configure apt
ENV DEBIAN_FRONTEND=noninteractive
RUN sudo apt-get update \
    && sudo apt-get -y install --no-install-recommends apt-utils 2>&1 \
# Install haskell ide engine dependencies
    && sudo apt-get -y install libicu-dev libtinfo-dev libgmp-dev \
# Clean up
    && sudo apt-get autoremove -y \
    && sudo apt-get clean -y \
    && sudo rm -rf /var/lib/apt/lists/* \
# Create symlink bind directory for build or haskell ide engine
    && mkdir -p $HOME/.local/bin \
# Install haskell ide engine
    && cd $HOME \
    && git clone https://github.com/haskell/haskell-ide-engine --recursive \
    && cd haskell-ide-engine \ 
    && sed -i "s/lts-[0-9][0-9].[0-9][0-9]/lts-16.5/" install/shake.yaml \
    && ./install.hs hie-8.8.3 \
    && export PATH="$PATH:/home/vscode/.local/bin/" \
    && stack install hoogle \
    && ./install.hs data \
    && rm -rf ../haskell-ide-engine
    
ENV PATH="${PATH}:/home/vscode/.local/bin/"

# Set the default shell to bash rather than sh
ENV SHELL /bin/bash



