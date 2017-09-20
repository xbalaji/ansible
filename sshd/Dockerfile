#
# available at gist: 
#   https://gist.github.com/xbalaji/ecd428eb8ee48981cb24ac0c57c8d21b
#
################## Dockerfile ###################
# from
#   https://docs.docker.com/engine/examples/running_ssh_service/
#
# build command
#   docker build -t ubuntu_sshd .
#

FROM ubuntu:16.04

RUN apt-get update && apt-get install -y openssh-server --no-install-recommends apt-utils
RUN mkdir /var/run/sshd
RUN echo 'root:balajiv' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

## add a new login 
## from: 
##       https://stackoverflow.com/questions/36490627/how-to-create-and-run-docker-container-with-new-user-other-than-root
#RUN export uid=1000 gid=1000 && \
#    mkdir -p /home/xbalaji && \
#    mkdir -p /etc/sudoers.d  && \
#    echo "xbalaji:x:${uid}:${gid}:xbalaji,,,:/home/xbalaji:/bin/bash" >> /etc/passwd && \
#    echo "xbalaji:x:${uid}:" >> /etc/group && \
#    echo "xbalaji ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/xbalaji && \
#    chmod 0440 /etc/sudoers.d/xbalaji && \
#    chown ${uid}:${gid} -R /home/xbalaji
#
#RUN echo 'xbalaji:balajiv' | chpasswd
#
#USER xbalaji
#WORKDIR /home/xbalaji
#


EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]

################## end - Dockerfile ###################
