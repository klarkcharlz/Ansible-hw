FROM ubuntu:latest

RUN apt-get update && \
    apt-get install -y \
    openssh-server \
    sudo \
    python3 \
    python3-pip \
    python3-apt \
    supervisor && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* 

RUN useradd -m ansible && \
    echo "ansible:ansible" | chpasswd && \
    adduser ansible sudo

RUN mkdir /var/run/sshd

RUN echo 'ansible ALL=(ALL) NOPASSWD: ALL' > /etc/sudoers.d/ansible

COPY id_ed25519.pub /home/ansible/.ssh/authorized_keys

RUN chown -R ansible:ansible /home/ansible/.ssh && \
    chmod 700 /home/ansible/.ssh && \
    chmod 600 /home/ansible/.ssh/authorized_keys

# Создаем директорию для конфигурации supervisord
RUN mkdir -p /etc/supervisor/conf.d

# Добавляем конфигурационный файл supervisord
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE 22

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/supervisord.conf"]
