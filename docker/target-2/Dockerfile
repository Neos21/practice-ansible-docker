FROM debian:buster

# OpenSSH をインストール・Ansible を実行するために Python をインストール・root ユーザでの SSH ログインを許可する
# - Debian 系向けにいくつかの設定を入れている
# - 操作前後の内容を出力するための `grep` を仕込んでいる
RUN set -x && \
    apt-get update && \
    apt-get install -y openssh-server xauth python && \
    mkdir /run/sshd && \
    grep 'PermitRootLogin' /etc/ssh/sshd_config && \
    sed -i 's/^#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    grep 'PermitRootLogin' /etc/ssh/sshd_config && \
    grep 'pam_loginuid.so' /etc/pam.d/sshd && \
    sed -i 's/session\s*required\s*pam_loginuid.so/session optional pam_loginuid.so/g' /etc/pam.d/sshd && \
    grep 'pam_loginuid.so' /etc/pam.d/sshd && \
    echo 'export VISIBLE=now' >> /etc/profile && \
    echo 'AddressFamily inet' >> /etc/ssh/sshd_config && \
    grep 'root' /etc/shadow && \
    echo 'root:mypassword' | chpasswd && \
    grep 'root' /etc/shadow

# sshd 向けに設定する
ENV NOTVISIBLE "in users profile"

# SSH ポートを公開する
EXPOSE 22

# sshd を起動する
CMD ["/usr/sbin/sshd", "-D"]
