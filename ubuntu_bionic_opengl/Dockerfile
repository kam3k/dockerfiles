FROM nvidia/opengl:1.0-glvnd-devel-ubuntu18.04

RUN apt-get update
RUN apt-get install -y sudo locales zsh git

# Add a user to the system
RUN useradd --create-home --shell /bin/zsh mgallant
RUN echo 'mgallant:letmein' | chpasswd

# Give this user sudo access
RUN addgroup mgallant sudo

COPY .ssh/* /home/mgallant/.ssh/
RUN chown mgallant:mgallant /home/mgallant/.ssh/* && chmod 600 /home/mgallant/.ssh/*
RUN chown mgallant:mgallant /home/mgallant/.ssh

# Clone my system setup scripts and dot files
USER mgallant
RUN mkdir -p /home/mgallant/.dot
RUN GIT_SSH_COMMAND="ssh -o StrictHostKeyChecking=no" git clone git@github.com:kam3k/dot_files.git /home/mgallant/.dot

# Run some scripts to setup the environment
USER root
ENV DEBIAN_FRONTEND=noninteractive
RUN /home/mgallant/.dot/install_packages.sh
RUN /home/mgallant/.dot/install_gui_packages.sh
USER mgallant
RUN /home/mgallant/.dot/post_install_setup.sh
USER root

# Generate the locale
RUN locale-gen en_US.UTF-8  

RUN apt-get clean

USER mgallant
# Set the locale
ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8

USER mgallant
WORKDIR /home/mgallant
