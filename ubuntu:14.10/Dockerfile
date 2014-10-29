FROM ubuntu:14.10

RUN apt-get update
RUN apt-get -y install curl
RUN curl -o /tmp/foo.deb http://opscode-omnibus-packages.s3.amazonaws.com/ubuntu/12.04/x86_64/chefdk_0.3.0-1_amd64.deb && dpkg -i /tmp/foo.deb && rm -f /tmp/foo.deb
RUN curl -o /tmp/foo.deb -k -L https://dl.bintray.com/mitchellh/vagrant/vagrant_1.6.5_x86_64.deb && dpkg -i /tmp/foo.deb && rm -f /tmp/foo.deb
RUN apt-get -y dist-upgrade
RUN apt-get -y install debootstrap openssh-server git-all subversion mercurial wget
RUN apt-get clean
RUN useradd -u 1001 -s /bin/bash jenkins
RUN printf "jenkins\njenkins\n" | passwd jenkins
#RUN su - jenkins -c '/opt/chefdk/embedded/bin/gem install knife-openstack kitchen-openstack'
#RUN su - jenkins -c 'vagrant plugin install vagrant-openstack-provider'
#RUN su - jenkins -c 'vagrant plugin install vagrant-berkshelf'

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
