FROM python:3.7.4-alpine3.10

LABEL maintainer="ctangarife" \
      description="Minimal Docker image with NSearch" \
      org.label-schema.url="" \
      org.label-schema.vcs-url="" \
      org.label-schema.vcs-type=""

RUN apk add --no-cache bash git openssh vim
RUN apk add --no-cache python3-dev libstdc++ 
RUN apk add --no-cache g++
RUN apk add --no-cache gcc wget \ 
        python3-dev musl-dev libc-dev libc6-compat \
        linux-headers build-base git libffi-dev openssl-dev \
        nmap nmap-scripts
RUN apk add --virtual build-dependencies build-base
RUN apk add --no-cache unzip readline-dev \
        sqlite-libs mariadb-dev sqlite-dev
RUN apk add --no-cache tzdata
RUN ln -s /usr/include/locale.h /usr/include/xlocale.h
RUN cp -r -f /usr/share/zoneinfo/America/Bogota /etc/localtime
RUN rm -rf /var/cache/apk/*


WORKDIR /var/www/

RUN git clone -b dev https://github.com/ctangarife/nsearch.git nsearch

ADD ./build/nsearch/config.yaml /var/www/nsearch/scripts/config.yaml

WORKDIR /var/www/nsearch

RUN pip install --upgrade pip

RUN pip install -r requirements.txt

RUN sh install.sh

RUN echo 'alias nsearch="python /var/www/nsearch/nsearch.py"' >> ~/.bashrc

CMD ["tail","-f","/dev/null"]