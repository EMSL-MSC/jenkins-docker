FROM centos:centos6

RUN yum -y install https://opscode-omnibus-packages.s3.amazonaws.com/el/6/x86_64/chefdk-0.3.0-1.x86_64.rpm
RUN yum -y install http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
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
RUN wget -O /etc/mock/mic-6-x86_64.cfg http://ceph-gw.emsl.pnl.gov/swift/v1/mock_cfg/mic-6-x86_64.cfg && wget -O /etc/mock/cloud-6-x86_64.cfg http://ceph-gw.emsl.pnl.gov/swift/v1/mock_cfg/cloud-6-x86_64.cfg
RUN service sshd start && service sshd stop

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
