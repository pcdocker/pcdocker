FROM pcdocker_django

ENV SFTP_USER docker
ENV SFTP_PASS changeme
ENV PASS_ENCRYPTED false

# PyCharm by default looks on /usr/bin/python
RUN ln -s /usr/local/bin/python /usr/bin/python

# Install setuptools, pip and OpenSSH
RUN \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get -y install python-pip python-setuptools python3-pip python3-setuptools openssh-server && \
    rm -rf /var/lib/apt/lists/*

# sshd needs this directory to run
RUN mkdir -p /var/run/sshd

# Copy configuration and entrypoint script
COPY sshd_config /etc/ssh/sshd_config
ADD .ssh_keys_to_docker/id_rsa.pub /ssh_id_rsa.pub

COPY entrypoint /

EXPOSE 22
EXPOSE 8000

ENTRYPOINT ["/entrypoint"]
