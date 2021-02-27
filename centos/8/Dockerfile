FROM centos:8

ENV container docker

RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == \
systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;

RUN dnf install -y python3 python3-pip gnupg2

RUN dnf update -y \
  	&& dnf clean all \
  	&& rm -rf /var/cache/yum

RUN python3 -m pip --no-cache-dir install --upgrade pip

RUN python3 -m pip --no-cache-dir install 'molecule[ansible,docker,lint]'

VOLUME [ "/sys/fs/cgroup" ]

CMD ["/usr/sbin/init"]