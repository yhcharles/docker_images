# Version: 0.0.1
FROM debian:jessie
MAINTAINER charlieyan

# set localtime
RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

RUN apt-get update

# install ssh service
# turn on port 36000
# set password
RUN (apt-get -qq install -y openssh-server && \
        mkdir -p /var/run/sshd && \
        sed -i "s/PermitRootLogin without-password/PermitRootLogin yes/" /etc/ssh/sshd_config && \
        sed -i "s/UsePrivilegeSeparation.*/UsePrivilegeSeparation no/g" /etc/ssh/sshd_config && \
        sed -i "s/UsePAM yes/UsePAM no/g" /etc/ssh/sshd_config && \
        sed -i "s/Port 22/Port 36000/" /etc/ssh/sshd_config && \
        echo "root:root" | chpasswd && \
        echo "alias ls='ls --color=auto'" >> /root/.bashrc && \
        echo "alias l='ls -l'" >> /root/.bashrc && \
        echo "alias ll='ls -al'" >> /root/.bashrc)

RUN apt-get -qq install -y default-jdk python python-gearman

EXPOSE 36000
CMD ["/usr/sbin/sshd", "-D"]

