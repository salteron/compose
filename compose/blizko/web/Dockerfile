FROM scratchy

# install curl and git
RUN apt-get install -y -q curl git vim

# install time command
RUN apt-get -y -q install time

# add GitHub to known hosts
RUN ssh-keyscan -H github.com >> /etc/ssh/ssh_known_hosts

# install ruby
ENV RVM_PATH /usr/local/rvm
ENV RVM ${RVM_PATH}/bin/rvm
ENV RVM_RUBY ruby-1.9.3-p545
RUN gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
RUN curl -L https://get.rvm.io | bash -s stable
RUN $RVM install $RVM_RUBY --patch railsexpress
ENV PATH ${RVM_PATH}/rubies/${RVM_RUBY}/bin:$PATH

# project deps
RUN apt-get install -y -q libxslt-dev libxml2-dev
RUN apt-get install -y -q libcurl3-dev
RUN apt-get install -y -q libpq-dev
RUN apt-get install -y -q libmagickwand-dev imagemagick
RUN apt-get install -y -q catdoc enca
