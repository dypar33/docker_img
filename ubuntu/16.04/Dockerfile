FROM ubuntu:16.04
LABEL maintainer="dypar33@gmail.com"
WORKDIR /root

RUN apt-get update

ARG DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Seoul 

RUN dpkg --add-architecture i386
RUN apt-get update
RUN apt-get install -y tzdata net-tools netcat curl wget git vim file gcc nasm nmap \
    gdb zsh libc6-i386 libc6-dev-i386 python3 python3-dev \
    ruby binwalk gcc-arm-linux-gnueabi g++-arm-linux-gnueabi \
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

RUN wget https://bootstrap.pypa.io/pip/3.5/get-pip.py
RUN python3 get-pip.py; rm -rf get-pip.py
RUN python3 -m pip install --upgrade pip setuptools
RUN python3 -m pip install --upgrade pwntools ropgadget pycrypto pycryptodome keystone-engine ropper gmpy gmpy2 pycryptodome

RUN git clone https://github.com/longld/peda.git ~/peda
RUN git clone https://github.com/scwuaptx/Pwngdb.git
RUN wget https://github.com/hugsy/gef/archive/refs/tags/2021.10.zip
RUN unzip ~/2021.10.zip
RUN echo "# source ~/peda/peda.py" >> ~/.gdbinit
RUN echo "source ~/gef-2021.10/gef.py" >> ~/.gdbinit
RUN sed -i 's/\\u27a4 />/g' ~/gef-2021.10/gef.py

RUN git clone https://github.com/zweisamkeit/RSHack.git
RUN ln -s /root/RSHack/rshack.py /usr/bin/rshack

RUN echo "set nu\nset autoindent\nset ts=4\nset sts=4\nset shiftwidth=4" >> ~/.vimrc

RUN mkdir workspace
WORKDIR /root/workspace/
# CMD ["/bin/zsh"]
CMD ["tail", "-f", "/dev/null"]
