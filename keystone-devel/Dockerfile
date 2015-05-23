FROM fedora:21
MAINTAINER michael mccune <msm@redhat.com>

RUN ["/usr/bin/yum", "install", "-y", \
     "git", \
     "python-setuptools", \
     "python-pip", \
     "python-lxml", \
     "python-greenlet-devel", \
     "python-ldap", \
     "sqlite-devel", \
     "openldap-devel", \
     "gcc", \
     "python-devel" \
    ]

WORKDIR /opt
RUN ["/usr/bin/git", "clone", "https://github.com/openstack/keystone"]

WORKDIR /opt/keystone
RUN ["/usr/bin/pip", "install", "-r", "requirements.txt"]
RUN ["/usr/bin/python", "setup.py", "install"]
RUN ["mkdir", "-p", "/etc/keystone"]
RUN ["cp", "etc/keystone.conf.sample", "/etc/keystone/keystone.conf"]
RUN ["cp", "etc/keystone-paste.ini", "/etc/keystone/"]
RUN ["cp", "etc/policy.json", "/etc/keystone/"]

EXPOSE 5000
EXPOSE 35357

ADD update_and_start_keystone /opt/

WORKDIR /
ENTRYPOINT ["/opt/update_and_start_keystone"]
