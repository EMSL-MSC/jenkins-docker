FROM centos:centos7

RUN yum -y install https://opscode-omnibus-packages.s3.amazonaws.com/el/6/x86_64/chefdk-0.3.0-1.x86_64.rpm
RUN yum -y install http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-2.noarch.rpm
RUN yum -y install https://dl.bintray.com/mitchellh/vagrant/vagrant_1.6.5_x86_64.rpm
RUN yum -y update
RUN yum -y install openssh-server java-1.7.0-openjdk-devel mock gcc-c++ gcc libffi-devel make git subversion mercurial wget yum-utils unzip && yum clean all
RUN useradd -u 1001 -g mock -s /bin/bash jenkins
RUN printf "jenkins\njenkins\n" | passwd jenkins
RUN su - jenkins -c '/opt/chefdk/embedded/bin/gem install knife-openstack kitchen-openstack'
RUN su - jenkins -c 'vagrant plugin install vagrant-openstack-provider'
RUN su - jenkins -c 'vagrant plugin install vagrant-berkshelf'
RUN sed -i 's/mockbuild.util.CLONE_NEWNS/0/' /usr/sbin/mock
RUN sed -i 's/\(.*ccache_enable.*\) = True/\1 = False/' /etc/mock/site-defaults.cfg
RUN sshd-keygen

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
