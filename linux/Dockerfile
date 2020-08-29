FROM centos:7

# system update
RUN yum -y update && yum clean all

# set locale
RUN yum reinstall -y glibc-common && yum clean all
ENV LANG ja_JP.UTF-8
ENV LANGUAGE ja_JP:ja
ENV LC_ALL ja_JP.UTF-8
RUN unlink /etc/localtime
RUN ln -s /usr/share/zoneinfo/Japan /etc/localtime
RUN localedef -f UTF-8 -i ja_JP ja_JP.UTF-8

# editor install
RUN yum install -y vim && yum clean all

# zsh
RUN yum install -y zsh

# make
RUN yum install -y make

# make directory for temp
RUN mkdir -p /home/tech/

# for zappa
RUN yum install -y gcc libffi-devel python-devel openssl-devel zlib-devel bzip2 bzip2-devel readline-devel sqlite sqlite-devel openssl-devel git
RUN curl -L https://bootstrap.pypa.io/get-pip.py | python
RUN curl -L https://raw.githubusercontent.com/yyuu/pyenv-installer/master/bin/pyenv-installer | bash


# the following to ~/.zshrc:
RUN echo '### virtualenv' >> ~/.zshrc
RUN echo 'export PATH="/root/.pyenv/bin:$PATH"' >> ~/.zshrc
RUN echo 'eval "$(pyenv init -)"' >> ~/.zshrc
RUN echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.zshrc

# install python & upgrade pip
RUN source ~/.zshrc && pyenv install 3.8.0 && pyenv global 3.8.0 && pip install -U pip

# install zappa
RUN source ~/.zshrc && pip install zappa