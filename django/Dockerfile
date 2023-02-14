FROM conda/miniconda3-centos7:latest
WORKDIR /app
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8
ENV TZ Asia/Shanghai
COPY .pip /root/.pip
COPY  ./yum.repos.d/nginx.repo /etc/yum.repos.d

RUN conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/ \
    && conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/ \
    && conda config --set show_channel_urls yes \
    && conda init \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone \
    && mkdir -p backend \
    && touch backend/start.sh

RUN yum install -y wget \
    && wget https://www.rarlab.com/rar/rarlinux-x64-5.9.0.tar.gz --no-check-certificate \
    && tar -zxf rarlinux-x64-5.9.0.tar.gz \
    && cp -r rar /usr/local/ \
    && ln -s /usr/local/rar/rar /usr/local/bin/rar \
    && ln -s /usr/local/rar/unrar /usr/local/bin/unrar \
    && rm rar* -rf

RUN yum install -y gcc gcc-c++ mariadb-devel rsync curl nginx epel-release bzip2 fontconfig bitmap-fonts bitmap-fonts-cjk crontabs dmidecode \
    && yum install -y unar p7zip p7zip-plugins \
    && yum clean all \
    && rm -rf /var/cache/yum


ENTRYPOINT ["/bin/sh","backend/start.sh"]
