#
# author: Balaji Venkataraman (http://bit.ly/xbalaji)
#
################## Dockerfile ###################
# from
#   https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux_atomic_host/7/html/getting_started_with_containers/using_red_hat_base_container_images_standard_and_minimal
#   https://github.com/CentOS/CentOS-Dockerfiles/tree/master/ssh/centos7
#
# build command
#   docker build -f <Dockerfile> -t rhel7ssh .
#
# prerequisites:
#
# docker pull registry.access.redhat.com/rhel7/rhel
# docker tag registry.access.redhat.com/rhel7/rhel:latest rhel7:latest
#

FROM rhel7:latest

RUN yum -y update; yum clean all
RUN yum -y install openssh-server passwd; yum clean all
RUN mkdir /var/run/sshd

RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key -N '' 

RUN echo -e "balajiv\nbalajiv" | (passwd --stdin root)
RUN echo ssh root password: balajiv


EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]

################## end - Dockerfile ###################
