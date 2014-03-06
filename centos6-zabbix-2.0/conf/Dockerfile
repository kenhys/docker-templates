FROM centos

MAINTAINER kenhys

RUN yum install sudo passwd openssh openssh-clients openssh-server httpd vim python-setuptools php php-devel php-mysql php-mbstring php-gd -y

RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
RUN sed -ri 's/#UsePAM no/UsePAM no/g' /etc/ssh/sshd_config

RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key
RUN ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key

RUN useradd docker
RUN echo 'docker:docker' | chpasswd
RUN echo 'docker ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers.d/docker

RUN easy_install supervisor
RUN echo_supervisord_conf > /etc/supervisord.conf
RUN echo '[include]' >> /etc/supervisord.conf
RUN echo 'files = supervisord/conf/*.conf' >> /etc/supervisord.conf
RUN mkdir -p /etc/supervisord/conf/
ADD supervisor.conf /etc/supervisord/conf/service.conf

EXPOSE 22 80

CMD ["/usr/bin/supervisord"]
