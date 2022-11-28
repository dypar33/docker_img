FROM ubuntu:19.04
LABEL maintainer="dypar33@gmail.com"
WORKDIR /root

RUN apt-get update

ARG DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Seoul 

RUN dpkg --add-architecture i386
RUN apt-get update
RUN apt-get install -y tzdata net-tools netcat curl wget git vim file gcc \
    gdb zsh libc6-i386 libc6-dev-i386 python2 python2-dev python3 python3-dev \
    python3-pip ruby binwalk gcc-arm-linux-gnueabi g++-arm-linux-gnueabi \
    build-essential libssl-dev libffi-dev libxml2-dev libxslt1-dev zlib1g-dev \
    gcc-aarch64-linux-gnu g++-aarch64-linux-gnu gdb-multiarch qemu-user-static 

# arm lib setting
RUN cp /usr/arm-linux-gnueabi/lib/ld-linux.so.3 /lib
RUN cp /usr/arm-linux-gnueabi/lib/libc.so.6 /lib
RUN cp /usr/arm-linux-gnueabi/lib/libgcc_s.so.1 /lib
RUN cp /usr/aarch64-linux-gnu/lib/ld-linux-aarch64.so.1 /lib

# zsh setting
RUN chsh -s `which zsh`
RUN curl -L https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh | sh
RUN git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ~/.oh-my-zsh/customs/plugins/zsh-syntax-highlighting
RUN git clone https://github.com/zsh-users/zsh-autosuggestions.git ~/.oh-my-zsh/customs/plugins/zsh-autosuggestions
RUN echo "source ~/.oh-my-zsh/customs/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ~/.zshrc
RUN echo "source ~/.oh-my-zsh/customs/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh" >> ~/.zshrc

RUN curl https://bootstrap.pypa.io/pip/2.7/get-pip.py --output get-pip.py
RUN python2 get-pip.py; rm -rf get-pip.py
RUN wget https://bootstrap.pypa.io/pip/3.5/get-pip.py
RUN python3 get-pip.py; rm -rf get-pip.py
RUN python2 -m pip install --upgrade pip setuptools
RUN python3 -m pip install --upgrade pip setuptools
RUN python3 -m pip install --upgrade pwntools ropgadget pycrypto pycryptodome
RUN gem install one_gadget

RUN git clone https://github.com/longld/peda.git ~/peda
RUN git clone https://github.com/scwuaptx/Pwngdb.git
RUN git clone https://github.com/hugsy/gef.git ~/gef
RUN echo "source ~/gef/gef.py" >> ~/.gdbinit

RUN git clone https://github.com/zweisamkeit/RSHack.git
RUN ln -s /root/RSHack/rshack.py /usr/bin/rshack

RUN mkdir workspace
WORKDIR /root/workspace/
CMD ["/bin/zsh"]