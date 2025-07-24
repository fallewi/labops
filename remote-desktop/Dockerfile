# Base Image
FROM nishanb/ck-x-simulator-vnc-base:v3

# Switch to root user for installations
USER 0

# Update and install required dependencies
RUN apt-get update && apt-get install -y \
    curl \
    wget \
    apt-transport-https \
    ca-certificates \
    gnupg \
    lsb-release \
    software-properties-common \
    ssh-client \
    telnet \
    nano \
    vim \
    curl \
    wget \
    xclip

#create datascientest user
RUN useradd -m datascientest

#set hostname as terminal
RUN echo "export HOSTNAME=terminal" >> /headless/.bashrc
#set terminal to bash
RUN echo "export TERM=xterm" >> /headless/.bashrc

#when shell open switch to datascientest user
RUN echo "cd /home/datascientest && su datascientest" >> /headless/.bashrc

#disable asking for ssh host verification
RUN mkdir -p /home/datascientest/.ssh
RUN touch /home/datascientest/.ssh/config
RUN echo "StrictHostKeyChecking no" >> /home/datascientest/.ssh/config
RUN echo "UserKnownHostsFile /dev/null" >> /home/datascientest/.ssh/config


# Copy startup script
COPY startup.sh /usr/local/bin/startup.sh
RUN chmod +x /usr/local/bin/startup.sh

COPY agent.py /tmp/agent.py

RUN sed -i '/### every exit != 0 fails the script/a /usr/local/bin/startup.sh' /dockerstartup/vnc_startup.sh