FROM kasmweb/core-debian-trixie:1.19.0
USER root

ENV HOME=/home/kasm-default-profile
ENV STARTUPDIR=/dockerstartup
ENV INST_SCRIPTS=$STARTUPDIR/install
WORKDIR $HOME

######### Customize Container Here ###########

RUN apt-get update && \
    apt-get install -y sudo && \
    echo "kasm-user ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers.d/kasm-user && \
    chmod 0440 /etc/sudoers.d/kasm-user && \
    rm -rf /var/lib/apt/lists/*

COPY public/background.png /usr/share/backgrounds/bg_default.png

RUN echo 'export PS1="\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ "' >> /etc/bash.bashrc && \
    echo 'export PS1="\\u@\\h:\\w\\$ "' >> /root/.bashrc

######### End Customizations ###########

RUN chown 1000:0 $HOME
RUN $STARTUPDIR/set_user_permission.sh $HOME

ENV HOME=/home/kasm-user
WORKDIR $HOME
RUN mkdir -p $HOME && chown -R 1000:0 $HOME

USER 1000